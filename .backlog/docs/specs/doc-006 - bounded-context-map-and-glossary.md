---
id: doc-006
title: bounded-context-map-and-glossary
type: specification
created_date: '2026-06-07 10:52'
tags:
  - specs
  - domain
  - bounded-contexts
  - glossary
---
# Bounded context map and glossary

## Tarkoitus

Tämä speksi määrittää projektin bounded contextit, vastuurajat ja yhteisen sanaston. Agentti käyttää tätä ennen käyttötapaus-, API-, data- tai integraatiosuunnittelua.

## Context map

### Auth

Auth omistaa käyttäjän identiteetin, kirjautumisen, sähköpostivahvistuksen, salasanan resetoinnin, käyttäjän hallinnollisen käyttötilan, roolin ja API-käyttöön tarvittavan principalin muodostamisen.

Auth ei omista sijoittaja- tai yritysdataa, ilmoitusten toimituskanavia, ulkoisten lähteiden datankeruuta eikä muiden bounded contextien datapoistoa.

### Notifications

Notifications omistaa käyttäjälle lähetettävät viestit, viestipohjat, kanavavalinnan ja toimituksen tilan. Auth saa pyytää sähköpostivahvistuksen tai salasanan resetoinnin toimitusta mutta ei saa päättää Notifications-kontekstin toimituspolitiikkaa.

Tuotantolähetys vaatii erillisen viestintäkanava-, lähettäjä-, salaisuus- ja auditointipäätöksen.

### Companies and watchlist

Companies and watchlist omistaa seurattavat suomalaiset yritykset, käyttäjän tai järjestelmän seurantalistan, yrityksen perustietojen hallinnan ja sen, mitä tietoa yrityksestä kerätään.

Tämä context käyttää YTJ-dataa adapterin kautta mutta ei saa vuotaa YTJ:n raakamallia julkiseen API:in tai domainiin.

### Marketdata

Marketdata omistaa seurattavien yritysten markkinadatan haun, tallennuksen, lähdeattribuution, päivityshetket ja datan esittämiseen tarvittavat kyselyt.

Marketdata käyttää EODHD:tä adapterin kautta. Se ei tuota sijoitusneuvontaa, kaupankäyntisignaaleja, suosituksia tai automaattisia kaupankäyntipäätöksiä.

### Comments

Comments omistaa hyväksytyistä keskustelulähteistä kerätyn keskusteluaineiston, lähdeattribuution, keruun tilan, deduplikoinnin ja keskusteluaineiston kyselyt.

Alkuvaiheen lähde on Inderes Forum. Tuotantokeruu on `Blocked`, kunnes käyttöehdot, robots-käytännöt, lisenssi ja lähdemainintavaatimus on tarkistettu.

### Scheduling

Scheduling omistaa ajastetut tausta-ajot, EventBridge-säännöt, keruiden käynnistyksen, uudelleenajon ja idempotenssin. Scheduling ei omista kerättävän datan domain-sääntöjä.

### Shared API boundary

Frontend käyttää backendin julkista API:a. API-sopimukset eivät saa sisältää AWS-, DynamoDB-, PynamoDB-, Pydantic-, EODHD-, YTJ- tai Inderes-raakamalleja.

## Glossary

- `User`: Auth-kontekstin käyttäjäidentiteetti.
- `Principal`: API-reunan validista JWT:stä muodostettu kutsujan identiteetti ja roolitieto use caseille.
- `Admin`: Auth-rooli, joka saa hallita käyttäjiä ja seurattavia yrityksiä hyväksyttyjen API-sopimusten mukaan.
- `Regular user`: Auth-rooli, joka saa tarkastella dataa roolinsa sallimissa rajoissa.
- `Tracked company`: yritys, jonka dataa järjestelmä kerää tai näyttää.
- `Watchlist`: seurattavien yritysten joukko ja keruuasetukset.
- `External source`: hyväksytty ulkoinen datalähde kuten EODHD, YTJ tai Inderes Forum.
- `Source attribution`: lähde, hakuajankohta ja lähteen oma tunniste, jotka tallennetaan ulkoisesta datasta.
- `Collection run`: ajastettu tai manuaalisesti käynnistetty datankeruun suoritus.
- `Mock-only integration`: adapteri ja testit on toteutettu, mutta tuotantokutsu ulkoiseen palveluun on estetty.

## Handoff rules

- Auth voi pyytää Notificationsia toimittamaan kertakäyttöisen salaisuuden mutta ei saa tallentaa plaintext-salaisuutta.
- Scheduling voi käynnistää Marketdata- ja Comments-keruita mutta ei saa ohittaa niiden kutsurajoja tai compliance-rajoja.
- Companies and watchlist määrittää mitä yrityksiä kerätään. Marketdata ja Comments päättävät vain oman datatyyppinsä keruusta.
- Ulkoisen lähteen adapteri normalisoi datan contextin domain-kielelle ennen tallennusta tai API-vastetta.

## Stop rules

Pysähdy ja pyydä päätös, jos:

- käyttötapaus kuuluu useaan contextiin eikä omistajuus ole selvä
- ulkoisen lähteen dataa tarvitaan tuotannossa ilman compliance-dokumentaatiota
- feature vaatii uutta contextia tai uuden jaetun domain-paketin
- API-sopimus yrittää palauttaa ulkoisen lähteen tai AWS-palvelun raakamallin
- käyttötapaus voisi tuottaa sijoitusneuvontaa, kaupankäyntisuosituksen tai automaattisen kaupankäyntipäätöksen

## Acceptance

- Agentti osaa nimetä käyttötapauksen omistavan contextin ennen suunnittelua.
- Agentti osaa nimetä handoffin, kun työ koskee useaa contextia.
- Agentti pysähtyy, jos omistajuus tai compliance-raja on epäselvä.
