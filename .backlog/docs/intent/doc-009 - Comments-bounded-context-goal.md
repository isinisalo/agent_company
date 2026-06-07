---
id: doc-009
title: Comments bounded context goal
type: other
created_date: '2026-06-07 12:36'
updated_date: '2026-06-07 12:44'
tags:
  - intent
  - goal
  - comments
---
# Comments bounded context goal

## GOAL

Tarjoa seurattavalle yritykselle rajattu ja lähdeattribuoitu keskusteluaineistonäkymä, joka perustuu yritykselle määritettyyn Inderes Forum -topiciin.

## INTENT

Comments-kontekstin tulee kerätä vain yritysseurannan kannalta hyväksyttyä keskusteluaineistoa, ei toimia yleisenä sosiaalisen median keräimenä. Keruun tulee olla deduplikoitua, cursorilla jatkettavaa, lähteeseen attribuoitua ja PII/compliance-rajojen mukaista.

Inderes Forum on alkuvaiheen keskustelulähde vain mock-only- ja compliance-rajauksen sisällä. Tuotantokeruu on sallittu vasta, kun käyttöehdot, kutsurajat, retention, PII-käsittely ja tekninen rajapinta on hyväksytty.

## CAPABILITIES

- Yritykseen liittyvän keskusteluaineiston haku yritykselle hyväksytyn topicin perusteella.
- Mock-only Inderes-vastauksen normalisointi Comments-kontekstin kielelle.
- Keskusteluaineiston deduplikointi ja tallennus lähdeattribuutiolla, hakuajankohdalla ja deduplikointirajalla.
- Yrityksen keskusteluaineiston rajattu näyttäminen käyttäjän oikeuksien mukaan.
- Keruun cursorin ja tilan tallennus niin, että seuraava keruu voi jatkua hallitusta rajasta.

## CONSTRAINTS

- Älä hae keskusteluaineistoa yritykselle, joka ei ole seurannassa tai jolle ei ole hyväksyttyä keskustelutopiccia.
- Älä vuodata raw Inderes -mallia domainiin, julkiseen API:in, fixtureihin tai lokiin.
- Älä tallenna tarpeetonta PII:tä tai käyttäjäsisältöä ilman eksplisiittistä käsittelyrajaa.
- Älä palauta tai lokita credentialeja, tokenillisia URL:eja tai raw-lähdevirheitä.
- Älä tee tuotantokeruuta, jos Inderes compliance -raja, käyttöehdot, kutsurajat, retention, PII-käsittely tai tekninen keruuraja puuttuvat.

## EVIDENCE

Comments etenee oikeaan suuntaan, kun mock-only-topic-haku, normalisointi, deduplikointi, tallennus, kysely, cursorin päivitys, virhetilat, PII-raja ja tuotantokeruun esto on testattu.
