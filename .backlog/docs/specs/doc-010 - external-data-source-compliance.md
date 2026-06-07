---
id: doc-010
title: external-data-source-compliance
type: specification
created_date: '2026-06-07 10:54'
updated_date: '2026-06-07 11:21'
tags:
  - specs
  - compliance
  - external-sources
  - data
---
# External data source compliance

## Tarkoitus

Tämä speksi määrittää ulkoisten lähteiden tuotantokäytön pysähtymisrajat. Se ei hyväksy tuotantokeruuta eikä päätä lähdekohtaisia ehtoja.

## Default state

EODHD, PRH:n YTJ Open Data API v3 ja Inderes Forum ovat `mock-only`, kunnes lähdekohtainen compliance-evidenssi on dokumentoitu ja hyväksytty.

`Mock-only` tarkoittaa, että agentti saa toteuttaa portin, adapterin, normalisoinnin, fixturet, Mockoon/response-testit ja lähdeattribuution. Agentti ei saa tehdä tuotantokutsua, ajastettua tuotantokeruuta tai oikeisiin credentialeihin perustuvaa ajoa.

## Required evidence

Ennen tuotantokäyttöä lähteelle pitää olla dokumentoitu vähintään:

- käyttötarkoitus järjestelmässä
- tarkistetut käyttöehdot, lisenssi tai muu käyttöoikeus
- lähdemainintavaatimus
- sallittu keruutiheys ja kutsuraja
- tallennus-, caching- ja retention-raja
- PII:n tai käyttäjäsisällön käsittelyraja, jos lähde sisältää niitä
- credentialin käsittely ja sijainti, jos credential tarvitaan
- virheenkäsittelyn ja retryjen raja
- vastuullinen hyväksyjä

## Source rules

EODHD on valittu markkinadatan lähdekandidaatiksi. Dataa ei saa käyttää sijoitusneuvontaan, suosituksiin tai kaupankäyntipäätöksiin.

YTJ on valittu suomalaisten yritysten perustietojen lähdekandidaatiksi. Henkilö- tai vastuuhenkilötiedot vaativat erillisen käsittelyrajan.

Inderes Forum on valittu alkuvaiheen keskusteluaineiston lähdekandidaatiksi. Tuotantokeruu on estetty, kunnes käyttöehdot, robots-käytäntö, lisenssi, lähdemaininta ja käyttäjäsisällön käsittelyraja on hyväksytty.

## Stop rules

Pysähdy, jos lähteen ehdot, lisenssi, robots-käytäntö, lähdemaininta, kutsuraja tai retention on epäselvä.

Pysähdy, jos tuotantokeruu tarvitsisi oikean credentialin.

Pysähdy, jos lähdedataa aiotaan käyttää sijoitusneuvontaan, suositukseen tai automaattiseen kaupankäyntipäätökseen.

## Acceptance

Agentti voi toteuttaa mock-only-adapterin ilman tuotantokäyttöönottoa.

Agentti estää tuotantokeruun ilman hyväksyttyä lähdekohtaista evidenssiä.

Agentti säilyttää lähdeattribuution ulkoisesta lähteestä normalisoituun dataan.
