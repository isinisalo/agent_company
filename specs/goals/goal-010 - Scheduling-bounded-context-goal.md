---
id: goal-010
title: Scheduling bounded context goal
type: other
created_date: '2026-06-07 12:36'
updated_date: '2026-06-07 12:45'
tags:
  - intent
  - goal
  - scheduling
---
# Scheduling bounded context goal

## GOAL

Tarjoa hallittu tausta-ajojen kyvykkyys, joka käynnistää yrityskohtaista tiedonkeruuta ajallaan, tallentaa ajon tilan ja estää tuotantokeruun silloin, kun lähteen tai ympäristön compliance-ehdot eivät täyty.

## INTENT

Scheduling-kontekstin tulee tehdä keruista toistettavia, idempotentteja ja operoitavia. Sen tehtävä on päättää milloin hyväksytty keruuajo on erääntynyt ja mikä ajon seuraava tila on, ei omistaa Companies-, Marketdata- tai Comments-domainlogiikkaa.

Scheduling toimii porttina tuotantokeruulle: vaikka adapteri olisi teknisesti kutsuttavissa, ajo ei saa edetä tuotantolähteeseen ilman hyväksyttyä credential-, kutsuraja-, retention-, käyttöehto-, IAM- ja deploy-rajaa.

## CAPABILITIES

- Keruuajastuksen määrittäminen hyväksytylle keruutyypille ja seurattavalle yritykselle tai yritysjoukolle.
- Erääntyneen keruuajon käynnistäminen idempotentisti.
- Keruuajon tuloksen, lähteen, hakuajankohdan, turvallisen virheluokan ja seuraavan tilan tallennus.
- Retry-kelpoisen virheen uudelleenyrityksen ajoitus hyväksyttyjen rajojen sisällä.
- Failed-tilan tallennus, kun retry-raja täyttyy tai virhe ei ole retry-kelpoinen.
- Compliance-puutteisen tuotantokeruun esto.

## CONSTRAINTS

- Älä luo päällekkäisiä hallitsemattomia ajoja samalle kohteelle ja keruutyypille.
- Älä ohita Companies/watchlist-kontekstin seuranta- ja keruuasetuksia.
- Älä ohita Marketdata- tai Comments-kontekstin mock-only- ja compliance-rajoja.
- Älä lokita credentialeja, API-avaimia, raw-lähdevirheitä, tarpeetonta PII:tä tai tokenillisia URL:eja.
- Älä toteuta tuotantoajastusta ilman hyväksyttyä deploy-, IAM-, EventBridge-, kutsuraja-, retention- ja operointisopimusta.
- Pysähdy, jos ajastus vaatii uutta AWS-palvelua, laajaa IAM-oikeutta tai production-deployta ilman hyväksyttyä päätöstä.

## EVIDENCE

Scheduling etenee oikeaan suuntaan, kun ajastuksen määrittäminen, erääntyneen ajon käynnistys, tuloksen tallennus, retry, failed-tila, idempotenssi, kutsurajojen kunnioitus ja compliance-puutteisen tuotantokeruun esto on testattu.
