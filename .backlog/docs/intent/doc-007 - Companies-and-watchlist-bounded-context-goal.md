---
id: doc-007
title: Companies and watchlist bounded context goal
type: other
created_date: '2026-06-07 12:36'
updated_date: '2026-06-07 12:44'
tags:
  - intent
  - goal
  - companies
  - watchlist
---
# Companies and watchlist bounded context goal

## GOAL

Tarjoa yritysseurantapalvelun ydin: hallittu lista suomalaisista seurattavista yrityksistä, niiden tunnisteista, perustiedoista ja keruuasetuksista.

## INTENT

Companies and watchlist -kontekstin tulee olla se paikka, josta muut contextit tietävät, mitä yrityksiä saa käsitellä ja millä keruuasetuksilla. Kontekstin tulee estää duplikaatit, epäselvät yritysidentiteetit ja ulkoisen lähdedatan vuotaminen domainin tai julkisen API:n raakamalliksi.

PRH:n YTJ Open Data API v3 toimii yritysten perustietolähteenä. Alkuvaiheen toteutus käyttää mock-only-adapteria, jotta yritysdataa voidaan normalisoida ja testata ilman tuotantokutsua.

## CAPABILITIES

- Seurattavan yrityksen lisääminen hyväksytyllä tunnisteella ja perusdatalla.
- Seurattavan yrityksen sallittujen tietojen ja keruuasetusten päivittäminen.
- Yrityksen poistaminen seurannasta vain määritellyn retention- ja deletion-sopimuksen mukaisesti.
- Seurattavien yritysten rajattu ja sivutettava listaus.
- Yrityksen perustietojen mock-only-päivitys YTJ-lähteestä.
- Lähteen ja hakuajankohdan säilyttäminen tallennetussa perustiedossa.

## CONSTRAINTS

- Älä lisää yritystä ilman hyväksyttyä yritystunnistetta ja admin-oikeutta.
- Älä muuta yrityksen identiteettiä päivitystoiminnolla ilman eksplisiittistä sopimusta.
- Älä poista yritystä tavalla, joka rikkoo Marketdata-, Comments- tai Scheduling-kontekstien retention- tai deletion-sopimusta.
- Älä vuodata YTJ:n raw-mallia domainiin, julkiseen API:in tai lokiin.
- Älä palauta tai lokita credentialeja, tokenillisia URL:eja, tarpeetonta PII:tä tai lähteen raw-dataa.
- Pysähdy, jos YTJ-tuotantokutsu, oikea credential, käyttöehtoevidenssi, kutsuraja tai retention-raja puuttuu.

## EVIDENCE

Companies and watchlist etenee oikeaan suuntaan, kun yrityksen lisäys, päivitys, poisto, listaus ja mock-only YTJ-perustietopäivitys on testattu validilla syötteellä, virheellisellä syötteellä, authorization-hylkäyksellä, duplikaattitapauksella, lähdeattribuutiolla ja salaisuuksien vuotamattomuudella.
