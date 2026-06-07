---
id: doc-011
title: Bounded context intent ja goal
type: other
created_date: '2026-06-07 11:40'
updated_date: '2026-06-07 11:41'
tags:
  - intent
  - goal
  - bounded-contexts
  - domain
---
# Bounded context intent ja goal

## Tarkoitus

Tämä dokumentti määrittää projektin bounded contextien intent- ja goal-tason rajaukset. Käytä tätä yhdessä `goal.md`:n, bounded context -kartan ja relevantin Backlog-tehtävän kanssa.

Dokumentti ei määritä contextien sisäisiä domain-malleja, API-reittejä, portteja, adaptereita, DynamoDB-avaimia, IAM-scopeja, event-skeemoja, infrastruktuuria tai frontend-näkymiä. HOW-tason ratkaisut kuuluvat detail-spec-tehtäviin ja tehtäväkohtaisiin implementation plan/notes/final summary -osioihin.

## Yleiset rajat

Järjestelmä ei saa tuottaa sijoitusneuvontaa, osto- tai myyntisuosituksia, kaupankäyntisignaaleja, automaattisia kaupankäyntipäätöksiä eikä kaupankäyntitoiminnallisuutta.

Ulkoiset lähteet ovat `mock-only`, kunnes lähdekohtainen compliance-evidenssi on dokumentoitu ja hyväksytty. Tämä koskee vähintään EODHD:tä, PRH:n YTJ Open Data API v3:a ja Inderes Forumia.

Salaisuuksia, credentialeja, tokeneita, password hasheja, token-digestejä, API-avaimia tai PII:tä ei saa palauttaa API-vastauksissa, julkaista eventeissä, tallentaa fixtureihin tai lokittaa.

Domain ei saa riippua AWS:n, HTTP:n, DynamoDB:n, FastAPI:n, Pydanticin, JWT-kirjaston tai ulkoisten API:en raakamalleista.

## Auth

### Goal

Varmista, että palvelua käyttävät vain tunnistetut ja oikeutetut käyttäjät rooliensa ja käyttötilansa sallimissa rajoissa.

### Intent

Auth omistaa käyttäjäidentiteetin, rekisteröinnin, kirjautumisen, sähköpostivahvistuksen, salasanan resetoinnin, käyttäjähallinnan, hallinnollisen käyttötilan ja API-käyttöön tarvittavan principalin.

Authin tehtävä on suojata palvelun käyttötapaukset niin, että muut contextit voivat tehdä päätöksiä validoidun principalin ja roolitiedon perusteella ilman, että ne omistavat käyttäjän tunnistamista.

### Out of scope

Auth ei omista ilmoitusten toimituskanavaa, sähköpostisisältöjen renderöintiä, seurattavia yrityksiä, markkinadataa, keskusteluaineistoa, ajastuksia eikä muiden contextien datapoistoa.

Auth ei saa paljastaa salasanoja, password hasheja, tokeneita, token-digestejä, JWT-sisältöjä tai muita credentialeja lokiin, fixtureihin, eventteihin tai API-vastauksiin.

## Notifications

### Goal

Toimita käyttäjälle järjestelmän pyytämät viestit luotettavasti ja tee viestien toimitustila jäljitettäväksi.

### Intent

Notifications omistaa käyttäjälle lähetettävät viestit, viestien renderöinnin, toimituspyynnöt ja toimituksen tilan.

Notificationsin tehtävä on vastaanottaa muiden contextien pyytämä viestintätarve ja muuttaa se käyttäjälle toimitettavaksi viestiksi valitun kanavan kautta hyväksyttyjen turvallisuus- ja compliance-rajojen sisällä.

### Out of scope

Notifications ei päätä, milloin Auth-, Companies and watchlist-, Marketdata-, Comments- tai Scheduling-context tarvitsee viestin. Kutsuva context omistaa viestin liiketoiminnallisen syyn ja sen, miksi viesti pitää lähettää.

Notifications ei saa sisällyttää viesteihin salaisuuksia, raw credentialeja tai tarpeetonta PII:tä. Tuotantotoimituskanava vaatii hyväksytyn tehtävän ja dokumentoidun konfiguraatio- sekä salaisuuskäsittelyn.

## Companies and watchlist

### Goal

Ylläpidä seurattavien suomalaisten yritysten joukkoa niin, että käyttäjä näkee, mitä yrityksiä palvelu seuraa ja mitä tietoja niistä kerätään.

### Intent

Companies and watchlist omistaa seurattavat yritykset, seurantalistan, yritysten perustietojen hallinnan ja yrityskohtaiset keruuasetukset.

Contextin tehtävä on toimia Marketdata- ja Comments-keruiden lähtökohtana: se määrittää, mitkä yritykset ovat järjestelmän seurannassa ja millä hyväksytyillä asetuksilla dataa saa hakea, tallentaa ja näyttää.

### Out of scope

Companies and watchlist ei omista markkinadatan arvoja, keskusteluaineiston sisältöä, ajastuksen teknistä suorittamista, käyttäjäidentiteettiä eikä ilmoitusten toimitusta.

YTJ-lähteen tuotantokäyttö on estetty, kunnes käyttöehdot, lähdemaininta, kutsurajat, retention, mahdollinen PII-käsittely ja credential-käsittely on dokumentoitu ja hyväksytty.

## Marketdata

### Goal

Hae, tallenna ja näytä seurattavien yritysten markkinadata niin, että käyttäjä voi tarkastella yrityskohtaisia tietoja samasta palvelusta ilman käsin tehtävää lähdehakua.

### Intent

Marketdata omistaa seurattavien yritysten markkinadatan keruun, normalisoinnin, tallennuksen, lähdeattribuution ja kyselyt.

Contextin tehtävä on käsitellä markkinadata omana datatyyppinään Companies and watchlist -contextin määrittämille yrityksille ja tarjota sitä näytettäväksi hyväksyttyjen lähde- ja turvallisuusrajojen sisällä.

### Out of scope

Marketdata ei omista seurantalistan yritysvalintaa, yrityksen perustietojen hallintaa, keskusteluaineistoa, ajastusten orkestrointia, käyttäjäidentiteettiä eikä ilmoitusten toimitusta.

Marketdata ei saa tuottaa sijoitusneuvontaa, suosituksia, kaupankäyntisignaaleja, automaattisia kaupankäyntipäätöksiä eikä reaaliaikaista streaming-markkinadataa alkuvaiheen tavoitteessa.

EODHD-tuotantokäyttö on estetty, kunnes käyttöehdot, lähdemaininta, kutsurajat, retention, credential-käsittely ja virheenkäsittelyn rajat on dokumentoitu ja hyväksytty.

## Comments

### Goal

Hae, tallenna ja näytä seurattaviin yrityksiin liittyvä keskusteluaineisto niin, että käyttäjä voi tarkastella yrityskohtaista keskustelua keskitetysti.

### Intent

Comments omistaa hyväksytyistä keskustelulähteistä kerätyn keskusteluaineiston, deduplikoinnin, normalisoinnin, tallennuksen, lähdeattribuution ja kyselyt.

Contextin tehtävä on pitää keskusteluaineisto erillään yrityksen perustiedoista ja markkinadatasta, mutta linkittää se seurattavaan yritykseen Companies and watchlist -contextin omistaman yritysvalinnan perusteella.

### Out of scope

Comments ei omista seurattavien yritysten perustietoja, markkinadataa, käyttäjäidentiteettiä, ajastusten teknistä suorittamista eikä ilmoitusten toimitusta.

Comments ei ole yleinen sosiaalisen median keräin. Alkuvaiheen keskustelulähde on Inderes Forum vain `mock-only`-tilassa, kunnes käyttöehdot, robots-käytäntö, lisenssi, lähdemaininta, käyttäjäsisällön käsittelyraja, kutsurajat ja retention on dokumentoitu ja hyväksytty.

## Scheduling

### Goal

Käynnistä ja seuraa ajastettuja tausta-ajoja niin, että yrityksiin liittyvät hyväksytyt keruut voidaan suorittaa toistettavasti ja niiden tila on jäljitettävä.

### Intent

Scheduling omistaa ajastetut tausta-ajot, keruiden käynnistyksen, uudelleenajon, idempotenssin ja collection run -tilan.

Contextin tehtävä on orkestroida, milloin hyväksytty keruu käynnistyy, ja pitää ajon tila erillään siitä datasta, jonka Marketdata tai Comments kerää ja tallentaa.

### Out of scope

Scheduling ei omista kerättävän datan domain-sääntöjä, yritysten seurantalistaa, markkinadatan normalisointia, keskusteluaineiston käsittelyä, käyttäjäidentiteettiä eikä ilmoitusten toimitusta.

Scheduling ei saa ohittaa lähdekohtaista compliance-rajaa. Ajastettu tuotantokeruu on estetty, kunnes kyseisen lähteen tuotantokäyttö ja keruutiheys on dokumentoitu ja hyväksytty.

## Acceptance

Agentti nimeää omistavan contextin ennen käyttötapauksen suunnittelua tai toteutusta.

Agentti kirjaa handoffin, kun työ koskee useaa contextia.

Agentti pysähtyy, jos käyttötapaus vaatii uuden contextin, jaetun domain-paketin, cross-context deletion -politiikan, tuotantokeruun hyväksymättömästä lähteestä tai sijoitusneuvonnan rajan tulkintaa.

Agentti pitää HOW-yksityiskohdat detail-spec-tehtävissä, ei tässä dokumentissa.
