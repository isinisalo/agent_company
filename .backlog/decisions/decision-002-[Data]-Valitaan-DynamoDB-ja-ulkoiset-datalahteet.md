---
id: decision-002
title: Valitaan DynamoDB ja ulkoiset datalähteet
date: '2026-06-06'
status: accepted
---
## Context
Järjestelmä tarvitsee hallitun tietokannan sekä lähteet markkinadataan, keskusteluaineistoon ja suomalaisten yritysten perustietoihin.

## Decision
Ensisijaiseksi tietokannaksi valitaan Amazon DynamoDB. Ulkoisiksi datalähteiksi valitaan EODHD markkinadataan, Inderes Forum keskusteluaineistoon ja PRH:n YTJ Open Data API v3 yritysten perustietoihin.

## Consequences

- DynamoDB-tietomalli suunnitellaan käyttötapausten hakumallien, avainten ja indeksien perusteella.
- Normaali käyttöliikenne ei saa perustua tauluskannauksiin tai ad hoc -relaatiokyselyihin.
- Ulkoiset datalähteet kapseloidaan adaptereihin, eivätkä lähdekohtaiset mallit saa vuotaa API-sopimuksiin tai domainiin.
- Tallennettuun ulkoiseen dataan liitetään lähde ja hakuajankohta.
- API-avaimet säilytetään Secrets Managerissa, ja integraatioissa määritellään aikakatkaisut, kutsurajat ja virheenkäsittely.
- Ulkoiset lähteet ovat testissä `mock-only`, tuotannossa käytetään live palveluita.

