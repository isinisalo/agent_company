---
id: doc-006
title: bounded-context-map-and-glossary
type: specification
created_date: '2026-06-07 10:52'
updated_date: '2026-06-07 11:20'
tags:
  - specs
  - domain
  - bounded-contexts
  - glossary
---
# Bounded context map and glossary

## Tarkoitus

Tämä speksi nimeää projektin bounded contextit ja omistajuusrajat. Se ei määritä contextien sisäistä domain-mallia, API-sopimusta, tietokantarakennetta tai infrastruktuuria. Nämä HOW-yksityiskohdat kuuluvat `Agent detail specifications` -milestonen tehtäviin.

## Context map

### Auth

Auth omistaa käyttäjäidentiteetin, rekisteröinnin, kirjautumisen, sähköpostivahvistuksen, salasanan resetoinnin, käyttäjän hallinnollisen käyttötilan ja API-käyttöön tarvittavan principalin.

Auth ei omista ilmoitusten toimituskanavaa, yritysdataa, markkinadataa, keskusteluaineistoa, ajastuksia eikä muiden contextien datapoistoa.

### Notifications

Notifications omistaa käyttäjälle lähetettävät viestit, viestien renderöinnin, toimituspyynnöt ja toimituksen tilan.

Notifications ei päätä, milloin Auth-, Companies-, Marketdata-, Comments- tai Scheduling-context tarvitsee viestin. Kutsuva context omistaa käyttötapauksen syyn.

### Companies and watchlist

Companies and watchlist omistaa seurattavat suomalaiset yritykset, seurantalistan, yrityksen perustietojen hallinnan ja keruuasetukset.

Tämä context käyttää YTJ-lähdettä adapterin kautta, kun tuotantokäytön compliance on hyväksytty.

### Marketdata

Marketdata omistaa seurattavien yritysten markkinadatan keruun, tallennuksen, lähdeattribuution ja kyselyt.

Marketdata ei tuota sijoitusneuvontaa, kaupankäyntisignaaleja, suosituksia tai automaattisia kaupankäyntipäätöksiä.

### Comments

Comments omistaa hyväksytyistä keskustelulähteistä kerätyn keskusteluaineiston, deduplikoinnin, tallennuksen, lähdeattribuution ja kyselyt.

Alkuvaiheen lähde on Inderes Forum vain mock-only-tilassa, kunnes compliance hyväksyy tuotantokeruun.

### Scheduling

Scheduling omistaa ajastetut tausta-ajot, keruiden käynnistyksen, uudelleenajon, idempotenssin ja collection run -tilan.

Scheduling ei omista kerättävän datan domain-sääntöjä eikä saa ohittaa lähdekohtaista compliance-rajaa.

## Shared language

- `User`: Auth-kontekstin käyttäjäidentiteetti.
- `Principal`: validoidusta kutsujasta muodostettu identiteetti ja roolitieto use caseille.
- `Admin`: rooli, joka saa hallita käyttäjiä ja seurattavia yrityksiä hyväksyttyjen tehtävien rajoissa.
- `Tracked company`: yritys, jonka dataa järjestelmä kerää tai näyttää.
- `Watchlist`: seurattavien yritysten joukko ja keruuasetukset.
- `External source`: EODHD, YTJ tai Inderes Forum.
- `Source attribution`: lähde, hakuajankohta ja lähteen tunniste, kun sellainen on saatavilla.
- `Collection run`: ajastettu tai manuaalinen datankeruun suoritus.
- `Mock-only`: adapteri ja testit voivat olla olemassa, mutta tuotantokutsu on estetty.

## Handoff rules

- Auth voi pyytää Notificationsia toimittamaan vahvistus- tai resetointiviestin, mutta ei päätä viestikanavan tuotantototeutusta.
- Companies and watchlist määrittää, mitä yrityksiä kerätään. Marketdata ja Comments vastaavat omista datatyypeistään.
- Scheduling käynnistää keruita, mutta keräävä context päättää datan normalisoinnista ja virhekäsittelystä.
- Ulkoisen lähteen raw-malli ei saa vuotaa domainiin, julkiseen API:in tai frontend-sopimukseen.

## Stop rules

Pysähdy, jos käyttötapaus kuuluu useaan contextiin eikä omistajuus ole selvä.

Pysähdy, jos feature vaatii uuden contextin, jaetun domain-paketin tai cross-context deletion -politiikan.

Pysähdy, jos ratkaisu voisi tuottaa sijoitusneuvontaa, suosituksia tai automaattisia kaupankäyntipäätöksiä.

## Acceptance

Agentti nimeää omistavan contextin ennen suunnittelua tai toteutusta.

Agentti kirjaa handoffin, kun työ koskee useaa contextia.

Agentti luo HOW-yksityiskohdat detail-spec-tehtävässä, ei tähän context map -dokumenttiin.
