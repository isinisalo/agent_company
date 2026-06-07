---
id: decision-011
title: '[Backend] Valitaan Auth REST API sopimus'
date: '2026-06-07 10:54'
status: accepted
---
## Context

Auth-käyttötapaukset tarvitsevat yhtenäisen julkisen REST API -sopimuksen ennen toteutusta. Sopimus kattaa rekisteröinnin, kirjautumisen, sähköpostivahvistuksen, salasanan resetoinnin ja admin-käyttäjähallinnan.

API-sopimuksen tulee olla riippumaton FastAPI-, Pydantic-, DynamoDB-, AWS- ja JWT-kirjastojen sisäisistä malleista. Domain ja application-kerros eivät saa lukea HTTP-headereita tai raakaa JWT:tä.

## Decision

Auth REST API julkaistaan versionoidun API-juuren alla:

```text
/api/v1
```

Kaikki JSON-vastaukset käyttävät `application/json`-sisältötyyppiä, ellei endpoint palauta `204 No Content`.

### Public auth endpoints

Rekisteröinti:

```text
POST /api/v1/auth/register
```

Request:

```json
{
  "email": "user@example.com",
  "username": "Example User",
  "password": "plaintext input only"
}
```

Success: `201 Created`

```json
{
  "user": {
    "id": "opaque user id",
    "email": "user@example.com",
    "username": "Example User",
    "role": "user",
    "emailVerificationState": "unverified",
    "adminAccessState": "enabled"
  }
}
```

Kirjautuminen:

```text
POST /api/v1/auth/login
```

Request:

```json
{
  "email": "user@example.com",
  "password": "plaintext input only"
}
```

Success: `200 OK`

```json
{
  "accessToken": "jwt",
  "tokenType": "Bearer",
  "expiresIn": 900,
  "user": {
    "id": "opaque user id",
    "email": "user@example.com",
    "username": "Example User",
    "role": "user"
  }
}
```

Sähköpostin vahvistus:

```text
POST /api/v1/auth/email-verifications/confirm
```

Request:

```json
{
  "email": "user@example.com",
  "token": "plaintext input only"
}
```

Success: `204 No Content`

Salasanan resetointipyyntö:

```text
POST /api/v1/auth/password-resets
```

Request:

```json
{
  "email": "user@example.com"
}
```

Success: `202 Accepted`

Resetointipyyntö palauttaa saman onnistumisvasteen riippumatta siitä, löytyykö käyttäjä.

Salasanan resetoinnin vahvistus:

```text
POST /api/v1/auth/password-resets/confirm
```

Request:

```json
{
  "email": "user@example.com",
  "token": "plaintext input only",
  "newPassword": "plaintext input only"
}
```

Success: `204 No Content`

### Admin endpoints

Admin-endpointit vaativat validin bearer-tokenin ja `admin`-roolin.

Käyttäjien listaus:

```text
GET /api/v1/admin/users?limit=50&cursor=<opaque cursor>
```

Success: `200 OK`

```json
{
  "items": [
    {
      "id": "opaque user id",
      "email": "user@example.com",
      "username": "Example User",
      "role": "user",
      "emailVerificationState": "verified",
      "adminAccessState": "enabled",
      "createdAt": "2026-06-07T00:00:00Z",
      "lastLoginAt": "2026-06-07T00:00:00Z"
    }
  ],
  "nextCursor": null
}
```

Käyttäjän käytön salliminen:

```text
POST /api/v1/admin/users/{userId}/enable
```

Success: `204 No Content`

Käyttäjän käytön estäminen:

```text
POST /api/v1/admin/users/{userId}/disable
```

Success: `204 No Content`

Käyttäjän poisto Auth-kontekstista:

```text
DELETE /api/v1/admin/users/{userId}
```

Success: `204 No Content`

Poisto on idempotentti myös silloin, kun käyttäjää ei löydy.

### Error format

Virheet palautetaan muodossa:

```json
{
  "error": {
    "code": "VALIDATION_ERROR",
    "message": "Request is invalid",
    "requestId": "correlation id"
  }
}
```

Sallitut yleiset koodit ovat:

- `VALIDATION_ERROR`
- `AUTHENTICATION_FAILED`
- `AUTHORIZATION_FAILED`
- `NOT_FOUND`
- `CONFLICT`
- `RATE_LIMITED`
- `INTERNAL_ERROR`

Kirjautumisen epäonnistuminen käyttää `AUTHENTICATION_FAILED`-koodia eikä paljasta, puuttuiko käyttäjä, oliko salasana väärä, oliko sähköposti vahvistamatta tai oliko käyttäjä estetty.

Salasanan resetointipyynnön `202 Accepted` ei paljasta käyttäjän olemassaoloa.

### JWT contract

Bearer-token välitetään headerissa:

```text
Authorization: Bearer <token>
```

API-reuna validoi allekirjoituksen, issuerin, audiencen, expirationin ja vaaditut claimit ennen use case -kutsua. Use case saa vain eksplisiittisen principalin.

Access tokenin oletusvoimassaoloaika on 900 sekuntia. Arvo luetaan Parameter Storesta. Refresh tokenit, revokointi, MFA ja sessiohallinta eivät kuulu tähän päätökseen.

V1-token allekirjoitetaan HS256-algoritmilla Secrets Managerissa säilytettävällä salaisuudella `agent-company/<env>/auth/jwt-signing-key`. Algoritmin vaihtaminen asymmetric key -malliin vaatii erillisen security- tai auth-päätöksen.

Vaaditut claimit:

- `sub`: käyttäjän opaque id
- `email`: käyttäjän sähköposti
- `role`: `user` tai `admin`
- `iss`: konfiguroitu issuer
- `aud`: konfiguroitu audience
- `iat`: issued-at
- `exp`: expiration
- `jti`: tokenin yksilöllinen tunniste

JWT:tä, allekirjoitusavainta tai claimien raakasisältöä ei saa lokittaa.

### CORS

CORS sallii vain eksplisiittisesti konfiguroidut origin-arvot. Wildcard-originia ei käytetä autentikoiduille reiteille.

## Consequences

- Käyttötapaustaskit voivat viitata tähän ADR:ään endpoint-, payload-, statuskoodi-, error- ja JWT-sopimuksen lähteenä.
- Domain ja application pysyvät irti HTTP-headerista, JWT-kirjastosta ja FastAPI/Pydantic-malleista.
- Admin-käyttäjähallinta kohdistuu opaque `userId`-tunnisteeseen, jonka admin saa listausvasteesta.
- Credential- ja token-kentät eivät palaudu missään API-vastauksessa.
- Resetointipyyntö ja kirjautumisen hylkäys eivät paljasta käyttäjän olemassaoloa tai tarkkaa tilaa.
- API-testeissä tulee kattaa onnistuneet vasteet, validointivirheet, authn/authz-hylkäykset, CORS-rajaus, JWT-claimien validointi ja credential-kenttien vuotamattomuus.
