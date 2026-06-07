---
id: decision-010
title: '[Data] Valitaan Auth DynamoDB tietokantarakenne'
date: '2026-06-07 10:54'
status: accepted
---
## Context

Auth-käyttötapaukset tarvitsevat DynamoDB-tietomallin, joka tukee käyttäjän luontia, kirjautumista sähköpostilla, sähköpostivahvistusta, salasanan resetointia, admin-käyttötilan muutoksia, käyttäjän poistoa ja käyttäjien sivutettua listausta.

Tietomallin tulee tukea yksilöllistä sähköpostia, idempotentteja ja ehdollisia kirjoituksia, credential-luokan tietojen vuotamattomuutta sekä agenttien kykyä toteuttaa käyttötapaukset ilman uusia datamallipäätöksiä.

## Decision

Auth käyttää yhtä bounded context -kohtaista DynamoDB-taulua. Taulun oletusnimi on `agent-company-<env>-auth-users`, ja nimi luetaan Parameter Storesta polusta `/agent-company/<env>/auth/users-table-name`.

Taulu käyttää yleisiä avainattribuutteja `PK` ja `SK`. Taulussa on vähintään seuraavat item-tyypit:

- User profile item: `PK = USER#<user_id>`, `SK = PROFILE`
- Email uniqueness item: `PK = EMAIL#<canonical_email>`, `SK = USER`

`user_id` on muuttumaton sisäinen tunniste. `canonical_email` on sähköpostin kanonisoitu muoto ja yksilöllisyyden lähde.

User profile item sisältää vähintään:

- `user_id`
- `canonical_email`
- `email_display`
- `username`
- `role`
- `email_verification_state`
- `admin_access_state`
- `password_hash`
- `password_hash_algorithm`
- `email_verification_digest`
- `email_verification_expires_at`
- `email_verification_used_at`
- `password_reset_digest`
- `password_reset_expires_at`
- `password_reset_used_at`
- `last_login_at`
- `login_count`
- `created_at`
- `updated_at`
- `version`
- `GSI1PK`
- `GSI1SK`

Email uniqueness item sisältää vähintään:

- `canonical_email`
- `user_id`
- `created_at`

Käyttäjien listaus käyttää GSI:tä:

- `GSI1PK = USER_LIST`
- `GSI1SK = <created_at>#<user_id>`

Admin-listauksen oletussivukoko on 50 ja enimmäissivukoko 100. Listaus palauttaa vain käyttäjäsummaryn eikä credential-, salasana-, token- tai digest-kenttiä.

Käyttäjän luonti tehdään DynamoDB transaction -kirjoituksena, joka luo sekä user profile itemin että email uniqueness itemin. Transaktio käyttää ehtoa, ettei `EMAIL#<canonical_email>` ole olemassa.

Sähköpostilla haku tehdään ensin email uniqueness itemillä ja sen jälkeen user profile itemillä. Normaali käyttöliikenne ei käytä tauluskannauksia.

Käyttäjän päivitykset käyttävät ehdollista kirjoitusta `version`-kenttää tai nykyistä salaisuusdigestin tilaa vasten. Sähköpostivahvistus ja salasanan resetoinnin vahvistus päivittävät käyttäjää vain, jos nykyinen digest on odotettu, expiry ei ole ylittynyt ja salaisuus on käyttämätön.

Käyttäjän poisto on Auth-kontekstissa idempotentti. Poisto poistaa user profile itemin ja email uniqueness itemin transaction-kirjoituksella, jos ne ovat olemassa. Poisto ei määritä muiden bounded contextien dataa, audit-retentiota tai anonymisointia.

Taulun TTL ei poista user profile itemeitä. Kertakäyttöisten salaisuuksien expiry tallennetaan attribuutteina ja tarkistetaan käyttötapauksessa. Erillinen cleanup tai token-sidecar-malli vaatii uuden tehtävän, jos sitä tarvitaan.

Tuotantotaulun oletuksena on on-demand-kapasiteetti, hallittu salaus ja Point-in-Time Recovery. Provisioned-kapasiteetti, single-table-malli usealle bounded contextille tai monialueinen replikointi vaatii erillisen päätöksen.

Salasanat, tokenien plaintext-arvot ja JWT:t eivät kuulu DynamoDB-tauluun. Tauluun tallennettavat password hashit ja token-digestit ovat credential-luokan dataa eivätkä koskaan palaudu API-vastauksissa, eventeissä, fixtureissä tai lokeissa.

## Consequences

- Auth-usecaset voivat toteuttaa `find by email`, `get by id`, `create`, `update`, `delete` ja `list users` -tarpeet ilman scan-operaatioita.
- Rekisteröinti voi estää duplicate email -käyttäjät ehdollisella transaction-kirjoituksella.
- Kirjautuminen löytää käyttäjän sähköpostilla ja päivittää vain `last_login_at`, `login_count`, `updated_at` ja `version`-kentät onnistuneessa kirjautumisessa.
- Sähköpostivahvistus ja resetoinnin vahvistus voidaan tehdä turvallisesti optimistic locking -periaatteella.
- Resetointipyyntö voi korvata aiemman käyttämättömän reset-digestin samalla käyttäjällä ilman uuden käyttäjän luontia.
- Admin-listaus on sivutettava ja rajattu, mutta yhden contextin `USER_LIST`-GSI-partition riittävyys pitää arvioida uudelleen, jos käyttäjämäärä kasvaa merkittävästi.
- DynamoDB-adapteritestien tulee todentaa transaction-create, duplicate email -hylkäys, sähköpostihaku, version-ehto, listauspaginointi, idempotentti poisto ja credential-kenttien puuttuminen summaryistä.
