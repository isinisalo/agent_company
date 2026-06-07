---
id: decision-009
title: Määritetään Auth bounded context ja usecase-sopimukset
date: '2026-06-07'
status: accepted
---
# Määritetään Auth bounded context ja usecase-sopimukset

## Context

Auth-kokonaisuuden ensimmäiset toteutustehtävät viittasivat puuttuvaan bounded context -spesifikaatioon. Ilman kanonista lähdettä agentti ei voi turvallisesti päättää käyttäjän identiteettiä, rooleja, tokenien käsittelyä, repositorioportteja, domain-tapahtumia tai resetointivirran turvallisuuskäyttäytymistä.

## CEO Decision

Tämä päätös korvaa puuttuvan bounded context -lähteen Auth bounded contextin kanonisena sopimuksena. TASK-002...TASK-011 toteutetaan tämän päätöksen, projektin tavoitteen, hyväksyttyjen ADR-päätösten ja agenttien päätöksenteon reunaehtojen mukaisesti.

## Decision

Auth MVP kattaa email+password-kirjautumisen, sähköpostivahvistuksen, kaksivaiheisen salasanan resetoinnin, JWT access tokenin ja admin-käyttäjähallinnan. Tämä milestone ei määritä refresh-tokenia, token-revokointia, SSO:ta, MFA:ta, passkey-tukea eikä tuotantosähköpostin toimitusmallia.

Domain ja application eivät saa riippua HTTP:stä, FastAPI:sta, Pydanticista, AWS SDK:sta, DynamoDB:stä, PynamoDB:stä, PyJWT:stä tai salasanahash-kirjastosta. HTTP, JWT-validointi, DynamoDB, Parameter Store, Secrets Manager ja viestien toimitus kuuluvat adaptereihin tai composition rooteihin.

`User` on Auth bounded contextin aggregate. Käyttäjän pysyvä identiteetti on normalisoitu `Email`, joka trimmataan, normalisoidaan pieniksi kirjaimiksi ja validoidaan syntaktisesti. Emailin toimituskelpoisuutta ei tarkisteta domainissa. Sama email saa esiintyä vain yhdellä käyttäjällä.

`User`-aggregaatin kanoninen tila on:

- `email`
- `name`
- `password_hash`
- `password_hash_algorithm`
- `role`
- `enabled`
- `email_verified_at`
- `verification_token_digest`
- `verification_token_expires_at`
- `reset_password_token_digest`
- `reset_password_token_expires_at`
- `last_login_at`
- `created_at`
- `updated_at`

`enabled` tarkoittaa adminin hallitsemaa käyttöeston tilaa. `email_verified_at` tarkoittaa sähköpostivahvistusta. Login onnistuu vain, kun käyttäjä on enabled-tilassa ja `email_verified_at` on asetettu.

Persistoitavat roolit ovat `READER` ja `ADMIN`. `GUEST` on vain autentikoimattoman kutsujan principal eikä sitä tallenneta käyttäjän rooliksi. Public registration luo käyttäjän roolilla `READER`; client ei saa asettaa `role`- tai `enabled`-arvoa.

Auth-domainin value objectit ovat `Email`, `Username`, `Password`, `EncryptedPassword`, `EmailVerificationToken`, `ResetPasswordToken` ja `Role`. `Username` vastaa käyttäjän `name`-kentän validointia. `Password` hyväksyy 12-256 merkkiä, hylkää tyhjän tai pelkkää whitespacea sisältävän arvon eikä pakota merkkiluokkasääntöjä. Salasanat hashataan Argon2idillä `PasswordHasher`-portin takana. Argon2id-yhteensopivan backend-adapterikirjaston lisääminen on tämän päätöksen perusteella sallittu, kun domain ja use caset eivät riipu kirjastosta.

Verification- ja reset-tokenit ovat kertakäyttöisiä satunnaisia arvoja. Plaintext-tokenia ei tallenneta, lokiteta eikä julkaista domain-eventissä. Aggregaatti tallentaa vain token-digestin ja vanhenemisajan. Tokenin toimitus käyttäjälle kuuluu erilliseen notification-sopimukseen tai paikalliseen testiadapteriin; tuotantosähköpostin toimitusmalli ei kuulu tähän milestoneen.

`IUserRepository`-portti tukee seuraavia operaatioita:

- `get_by_email(email)`: palauttaa käyttäjän tai nostaa domain/application-tason not found -virheen.
- `find_by_email(email)`: palauttaa käyttäjän tai `None`.
- `create(user)`: luo käyttäjän ehdollisesti ja estää duplikaatti-emailin.
- `update(user)`: tallentaa muutetun käyttäjän ehdollisesti.
- `delete_by_email(email)`: poistaa käyttäjän idempotentisti.
- `list_users(limit, cursor)`: palauttaa käyttäjäsummary-sivun ilman salasana- tai token-digest-kenttiä.

`EventBus.publish` hyväksyy vain `DomainEvent`-sopimuksen mukaisen tapahtuman. Domain-eventin peruskentät ovat `event_id`, `event_type`, `version`, `occurred_at`, `correlation_id`, `causation_id` ja `payload`. Event payload ei saa sisältää plaintext-salasanaa, password hashia, tokenia, token-digestiä, JWT:tä tai salaisuuksia.

`SettingsStore.is_feature_enabled(path)` palauttaa boolean-arvon. Polku `/feature/auth/register_user` ohjaa public registrationia. Jos arvo puuttuu, sitä ei voi lukea tai sitä ei voi tulkita booleaniksi, tulos on `false` ja rekisteröinti hylätään hallitulla virheellä.

Resetointi on kaksivaiheinen:

1. `RequestPasswordReset` hyväksyy sähköpostin ja palauttaa aina saman `202 Accepted` -vastauksen riippumatta siitä, onko käyttäjä olemassa. Olemassa olevalle käyttäjälle tallennetaan reset-token-digest ja julkaistaan tokeniton `PasswordResetRequested`-domain-event.
2. `ConfirmPasswordReset` hyväksyy emailin, tokenin ja uuden salasanan. Se validoi tokenin digestiä ja vanhenemisaikaa vasten, vaihtaa salasanan, tyhjentää reset-token-digestin ja hylkää uudelleenkäytetyn tai virheellisen tokenin.

Admin-käyttäjähallinnan endpointit vaativat `ADMIN`-roolin. `ListUsers` ei saa palauttaa `password_hash`, `verification_token_digest`, `reset_password_token_digest` tai muita credential-kenttiä.

## Consequences

- TASK-002 on Auth-perustan toteutustehtävä, ei paikka tehdä uusia auth-arkkitehtuuripäätöksiä.
- TASK-003...TASK-011 viittaavat tähän päätökseen kanonisena Auth-sopimuksena.
- Vanha bounded context -lähteen blocker on ratkaistu tällä päätöksellä.
- Tokenien toimitus, audit-retentio, privacy-poistopolitiikka, refresh-tokenit ja tuotantoviestintä vaativat erilliset hyväksytyt speksit tai tehtävät ennen tuotantolaajennusta.

## References

- OWASP Password Storage Cheat Sheet: https://cheatsheetseries.owasp.org/cheatsheets/Password_Storage_Cheat_Sheet.html
- OWASP Forgot Password Cheat Sheet: https://cheatsheetseries.owasp.org/cheatsheets/Forgot_Password_Cheat_Sheet.html
