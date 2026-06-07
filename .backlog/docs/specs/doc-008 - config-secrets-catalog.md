---
id: doc-008
title: config-secrets-catalog
type: specification
created_date: '2026-06-07 10:53'
tags:
  - specs
  - config
  - secrets
  - aws
---
# Config and secrets catalog

## Tarkoitus

Tämä speksi määrittää, mitkä arvot ovat konfiguraatiota, mitkä salaisuuksia, miten ne nimetään ja milloin agentin pitää pysähtyä. Tämä dokumentti ei sisällä oikeita arvoja.

## Storage rules

Parameter Store sisältää ei-salaisen ympäristökohtaisen konfiguraation:

- DynamoDB-taulunimet
- sallitut CORS-originien listat
- feature flagit
- kutsurajat ja aikakatkaisut
- polling- ja schedule-välit
- ulkoisten palvelujen ei-salaiset endpointit
- JWT issuer ja audience, jos niiden paljastuminen ei vaaranna järjestelmää

Secrets Manager sisältää salaisuudet ja credential-luonteiset arvot:

- JWT-allekirjoitusavaimet
- API-avaimet ja palvelutunnukset
- webhook-salaisuudet
- private keyt
- ulkoisten palvelujen tokenit
- arvot, joiden luokka on epäselvä

SecureString-parametria käytetään vain erillisellä infra- tai security-päätöksellä. Oletus on: salaisuudet Secrets Manageriin ja ei-salainen konfiguraatio Parameter Storeen.

## Naming

Ympäristöt ovat `dev`, `test` ja `prod`, ellei infra-spekseissä päätetä toisin.

Parameter Store -polun muoto on:

```text
/<app>/<env>/<context>/<name>
```

Oletus `<app>` on `agent-company` AWS-resurssien ja parametripolkujen nimissä.

Secrets Manager -nimen muoto on:

```text
<app>/<env>/<context>/<secret-name>
```

Parametrin tai salaisuuden nimestä pitää selvitä käyttötarkoitus ilman arvon lukemista.

## Minimum catalog

### Auth

- Parameter Store: `/agent-company/<env>/auth/users-table-name`
- Parameter Store: `/agent-company/<env>/auth/jwt-issuer`
- Parameter Store: `/agent-company/<env>/auth/jwt-audience`
- Parameter Store: `/agent-company/<env>/auth/access-token-ttl-seconds`
- Parameter Store: `/agent-company/<env>/auth/register-user-enabled`
- Parameter Store: `/agent-company/<env>/auth/verification-token-ttl-seconds`
- Parameter Store: `/agent-company/<env>/auth/password-reset-token-ttl-seconds`
- Secrets Manager: `agent-company/<env>/auth/jwt-signing-key`

### API boundary

- Parameter Store: `/agent-company/<env>/api/allowed-cors-origins`
- Parameter Store: `/agent-company/<env>/api/public-base-url`

### Notifications

- Parameter Store: `/agent-company/<env>/notifications/from-address`
- Parameter Store: `/agent-company/<env>/notifications/public-action-base-url`
- Secrets Manager: `agent-company/<env>/notifications/provider-credentials`

Notifications tuotantolähetys on `Blocked`, kunnes provider, lähettäjä, domain-verifiointi, bounce-käsittely ja salaisuusmalli on päätetty.

### External sources

- Secrets Manager: `agent-company/<env>/marketdata/eodhd-api-key`
- Parameter Store: `/agent-company/<env>/marketdata/eodhd-base-url`
- Parameter Store: `/agent-company/<env>/marketdata/eodhd-rate-limit`
- Parameter Store: `/agent-company/<env>/companies/ytj-base-url`
- Parameter Store: `/agent-company/<env>/comments/inderes-base-url`
- Parameter Store: `/agent-company/<env>/comments/inderes-rate-limit`

EODHD-, YTJ- ja Inderes-tuotantokäyttö on `Blocked`, kunnes compliance-speksi hyväksyy lähteen käytön.

## Runtime behavior

Pakollisen parametrin puuttuminen aiheuttaa käynnistys- tai käyttötapauskohtaisen virheen. Virhe saa nimetä puuttuvan parametrin mutta ei saa sisältää salaisia arvoja.

Salaisuuksia ei saa tulostaa, lokittaa, tallentaa fixtureihin, lisätä `.env`-esimerkkeihin tai palauttaa API-vastauksissa.

Lambda saa lukea vain oman käyttötapauksensa tarvitsemat parametrit ja salaisuudet. IAM-politiikka rajataan parametripolkuun tai salaisuuden ARNiin.

## Stop rules

Pysähdy ja pyydä päätös, jos:

- arvo voi olla salaisuus
- uusi salaisuus tarvitsee kierrätysmallin
- Lambda tarvitsee laajan lukuoikeuden usean contextin parametreihin tai salaisuuksiin
- tuotantoarvoa tarvitaan paikallisessa testissä
- salaisuuden nimi, sijainti tai lukija on epäselvä

## Acceptance

- Agentti osaa valita Parameter Storen ja Secrets Managerin välillä.
- Agentti osaa nimetä uuden arvon ympäristö- ja context-kohtaisesti.
- Agentti pysähtyy ennen epäselvän tai laajasti jaetun salaisuuden lisäämistä.
