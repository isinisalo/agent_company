---
id: goal-008
title: Marketdata bounded context goal
type: other
created_date: '2026-06-07 12:36'
updated_date: '2026-06-07 12:44'
tags:
  - intent
  - goal
  - marketdata
---
# Marketdata bounded context goal

## GOAL

Tarjoa seurattavalle yritykselle lähdeattribuoitu markkinadatanäkymä, joka perustuu EODHD-lähteestä haettuun ja Marketdata-kontekstin kielelle normalisoituun dataan.

## INTENT

Marketdata-kontekstin tulee tehdä markkinadatasta jäljitettävää, turvallisesti kyseltävää ja yritysseurantaan riittävää ilman sijoitusneuvontaa tai kaupankäyntitoiminnallisuutta. Konteksti ei saa tehdä EODHD:n raw-mallista domain- tai API-sopimusta.

Alkuvaiheen toteutus käyttää mock-only EODHD-adapteria. Tuotantokäyttö on sallittu vasta, kun credentialit, kutsurajat, käyttöehdot, aikakatkaisut, retention ja virheluokat on hyväksytty.

## CAPABILITIES

- Markkinadatan haku vain Companies/watchlist-kontekstissa seurattavalle yritykselle.
- Mock-only EODHD-vastauksen normalisointi Marketdata-kontekstin kielelle.
- Normalisoidun markkinadatan tallennus lähdeattribuutiolla ja hakuajankohdalla.
- Yrityksen markkinadatasummaryn rajattu näyttäminen käyttäjän oikeuksien mukaan.
- Lähdevirheiden, kutsurajojen ja uudelleenkäsittelyn turvallinen käsittely.

## CONSTRAINTS

- Älä hae markkinadataa yritykselle, joka ei ole seurannassa.
- Älä palauta sijoitusneuvontaa, osto- tai myyntisuosituksia tai kaupankäyntipäätöksiä.
- Älä vuodata raw EODHD -mallia domainiin, julkiseen API:in, fixtureihin tai lokiin.
- Älä palauta tai lokita API-avaimia, credentialeja, tokenillisia URL:eja tai raw-lähdevirheitä.
- Älä salli saman lähdedatan uudelleenkäsittelyn korruptoida tallennettua dataa tai luoda hallitsemattomia duplikaatteja.
- Pysähdy tai estä haku, jos tuotantokutsu, credential, kutsuraja, käyttöehtoevidenssi, retention tai compliance-raja puuttuu.

## EVIDENCE

Marketdata etenee oikeaan suuntaan, kun mock-only-haku, normalisointi, tallennus, kysely, lähdeattribuutio, duplikaattien hallinta, lähdevirheet, kutsurajat ja sijoitusneuvonnan poissulku on testattu.
