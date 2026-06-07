---
id: doc-007
title: security-data-classification
type: specification
created_date: '2026-06-07 10:53'
updated_date: '2026-06-07 11:20'
tags:
  - specs
  - security
  - data
  - privacy
---
# Security data classification

## Tarkoitus

Tämä speksi määrittää dataluokkien ja vuotamattomuuden vähimmäisrajat. Se ei päätä context-kohtaisia retention-, audit- tai poistopolitiikkoja; ne kuuluvat detail-spec-tehtäviin tai käyttäjän päätökseen.

## Data classes

`Public product data` on ei-salaista sovellus- ja käyttöliittymäsisältöä, jota saa commitoida, jos se ei sisällä PII:tä, credentialeja, sisäisiä resursseja tai lisenssirajoitettua raakadataa.

`External source data` on EODHD-, YTJ- tai Inderes-lähteestä peräisin olevaa dataa. Tallennettuun ulkoiseen dataan liitetään lähde ja hakuajankohta, kun dataa saa tuotantokäyttää.

`User PII` sisältää vähintään sähköpostin, nimen, käyttäjätunnuksen, IP-osoitteen ja tunnistettavan käyttäjäkontekstin. PII:tä tallennetaan vain hyväksytyn käyttötapauksen tarpeeseen.

`Credentials and secrets` sisältää plaintext-salasanat, password hashit, tokenit, token-digestit, JWT:t, allekirjoitusavaimet, API-avaimet, private keyt ja ulkoisten palvelujen tunnukset.

`Operational telemetry` sisältää lokit, metriikat ja trace-tiedot. Telemetria saa sisältää käyttötapauksen, tuloksen, error-luokan ja korrelaatiotunnisteen, mutta ei salaisuuksia tai credentialeja.

## Non-disclosure rules

Credentialeja ja salaisuuksia ei saa commitoida, palauttaa API-vastauksessa, julkaista eventissä, tallentaa fixtureen tai lokittaa.

PII:tä ei saa lisätä lokiin, fixtureen, virhevastaukseen tai domain-eventtiin ilman eksplisiittistä käyttötapaustarvetta ja sanitointia.

Ulkoisen lähteen raw-malli ei saa vuotaa domainiin, frontendille tai julkiseen API-sopimukseen.

## Stop rules

Pysähdy, jos uuden kentän dataluokka on epäselvä.

Pysähdy, jos muutos tallentaisi uuden PII- tai credential-kentän ilman detail-speciä tai hyväksyttyä tehtävää.

Pysähdy, jos poisto, anonymisointi, audit trail tai retention vaikuttaa useaan bounded contextiin.

Pysähdy, jos ratkaisu voisi tuottaa sijoitusneuvontaa, suosituksia tai automaattisia kaupankäyntipäätöksiä.

## Acceptance

Agentti luokittelee uuden kentän ennen tallennusta tai palauttamista.

Agentti pystyy perustelemaan, saako kenttä näkyä API-vastauksessa, eventissä, fixtureissä tai lokissa.

Agentti kirjaa security- ja data-rajoitukset taskin final summaryyn, kun muutos koskee näitä luokkia.
