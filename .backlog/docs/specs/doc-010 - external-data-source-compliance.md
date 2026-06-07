---
id: doc-010
title: external-data-source-compliance
type: specification
created_date: '2026-06-07 10:54'
tags:
  - specs
  - compliance
  - external-sources
  - data
---
# External data source compliance

## Tarkoitus

Tämä speksi määrittää EODHD-, YTJ- ja Inderes Forum -lähteiden tuotantokäytön ehdot agenttityölle. Dokumentti ei hyväksy tuotantokeruuta sellaisenaan. Se määrittää, mitä pitää todentaa ennen tuotantokäyttöä.

## Default state

Kaikki ulkoiset datalähteet ovat `mock-only`, kunnes lähdekohtainen compliance-evidenssi on kirjattu ja hyväksytty.

`mock-only` tarkoittaa:

- adapterin portti, domain-normalisointi ja testit saa toteuttaa
- Mockoon-, responses- tai fixture-pohjaiset testit saa lisätä
- tuotantokutsua, ajastettua keruuta tai oikeiden credentialien käyttöä ei saa ottaa käyttöön
- tallennusmalli saa sisältää lähdeattribuution ja fetched-at-kentät

## Required evidence per source

Ennen tuotantokäyttöä lähteelle kirjataan vähintään:

- lähteen nimi ja käyttötarkoitus
- käyttöehtojen tai lisenssin tarkistuspäivä
- sallittu käyttötapa järjestelmässä
- kielletty käyttötapa järjestelmässä
- lähdemainintavaatimus
- rate limit tai konservatiivinen kutsuraja
- caching- ja retention-raja
- credentialin sijainti Secrets Managerissa, jos credential tarvitaan
- virheenkäsittely ja retry-raja
- vastuullinen hyväksyjä

Jos lähteen ehdot muuttuvat tai ovat epäselvät, tuotantokäyttö palautuu `mock-only`-tilaan.

## EODHD

EODHD on valittu markkinadatan lähteeksi. Ennen tuotantokäyttöä pitää todentaa:

- lisenssi sallii suunnitellun tallennuksen ja näyttämisen
- lähdemaininta täyttää EODHD:n vaatimukset
- API-avaimen säilytys on Secrets Managerissa
- kutsurajat ja retryt eivät riko palvelun ehtoja
- dataa ei käytetä sijoitusneuvontaan, suosituksiin tai kaupankäyntipäätöksiin

Marketdata-adapteri ei saa vuotaa EODHD:n raakamallia domainiin tai julkiseen API:in.

## YTJ Open Data API v3

YTJ on valittu suomalaisten yritysten perustietojen lähteeksi. Ennen tuotantokäyttöä pitää todentaa:

- lisenssi ja lähdemainintavaatimus
- sallitut tallennettavat kentät
- henkilötietojen tai vastuuhenkilötietojen käsittelyn rajat
- retention ja päivitystiheys
- virheiden ja puuttuvan datan käsittely

Companies and watchlist -context normalisoi YTJ-datan omaan domain-kieleensä.

## Inderes Forum

Inderes Forum on valittu alkuvaiheen keskusteluaineiston lähteeksi. Tuotantokeruu on `Blocked`, kunnes seuraavat on tarkistettu:

- käyttöehdot
- robots-käytännöt
- lisenssi tai muu käyttöoikeus
- lähdemainintavaatimus
- sallittu keruutiheys
- sallittu säilytysaika
- käyttäjäsisällön ja mahdollisen PII:n käsittelyrajat

Comments-kontekstin adapteri saa olla olemassa mockattuna. Ajastettu tuotantokeruu ei saa käynnistyä ennen hyväksyttyä compliance-päätöstä.

## Source attribution

Kaikessa ulkoisesta lähteestä tallennetussa datassa tulee olla:

- `source` tai domainin vastaava lähdetieto
- `fetched_at` UTC ISO 8601 -muodossa
- lähteen oma tunniste, kun sellainen on saatavilla
- normalisoidun datan schema-versio, jos mallia muutetaan ajan yli

Lähdeattribuutiota ei saa hävittää myöhemmissä muunnoksissa.

## Stop rules

Pysähdy ja pyydä päätös, jos:

- lähteen ehdot, robots-käytäntö, lisenssi tai lähdemaininta on epäselvä
- tuotantokeruu tarvitsisi oikean credentialin
- ajastusväliä ei voi perustella kutsurajojen perusteella
- lähde sisältää PII:tä tai käyttäjäsisältöä eikä käsittelyrajaa ole hyväksytty
- dataa aiotaan käyttää suositukseen, sijoitusneuvontaan tai kaupankäyntipäätökseen

## Acceptance

- Agentti voi toteuttaa mockatun adapterin ilman tuotantokäyttöönottoa.
- Agentti ei voi käynnistää tuotantokeruuta ilman lähdekohtaista hyväksyttyä evidenssiä.
- Agentti tallentaa lähdeattribuution kaikkeen ulkoisesta lähteestä normalisoituun dataan.
