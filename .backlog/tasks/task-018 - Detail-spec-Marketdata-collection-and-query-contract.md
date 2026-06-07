---
id: TASK-018
title: 'Detail spec: Marketdata collection and query contract'
status: To Do
assignee: []
created_date: '2026-06-07 11:23'
labels:
  - Marketdata
  - Spec
  - Backend
milestone: m-3
dependencies:
  - TASK-014
  - TASK-017
documentation:
  - .backlog/docs/intent/goal.md
  - .backlog/docs/governance/Agenttien päätöksenteon reunaehdot.md
  - .backlog/docs/specs/doc-006 - bounded-context-map-and-glossary.md
  - .backlog/docs/specs/doc-010 - external-data-source-compliance.md
priority: medium
ordinal: 2300
---

## Description

<!-- SECTION:DESCRIPTION:BEGIN -->
### MITÄ
Määritä Marketdata bounded contextin HOW-tason keruu-, tallennus-, kysely-, EODHD-adapteri- ja testisopimus hyväksyttyjen projektirajojen sisällä.

Specin pitää tukea markkinadatan hakua seurattavalle yritykselle, lähdeattribuutiota, datan katselua sekä lähdevirheiden ja kutsurajojen käsittelyä.

### MIKSI
Marketdata on keskeinen osa seurattavan yrityksen näkymää, mutta se ei saa muuttua sijoitusneuvonnaksi tai EODHD-raakamallin julkaisuksi.
<!-- SECTION:DESCRIPTION:END -->

## Acceptance Criteria
<!-- AC:BEGIN -->
- [ ] #1 GIVEN Marketdata detail-spec tehdään, WHEN tehtävä valmistuu, THEN spec kuvaa keruun, tallennuksen ja kyselyjen vastuut käyttötapausten kannalta riittävästi.
- [ ] #2 GIVEN EODHD-adapteria suunnitellaan, WHEN spec luetaan, THEN raw EODHD -malli ei vuoda domainiin tai julkiseen API:in.
- [ ] #3 GIVEN markkinadata tallennetaan, WHEN spec tarkistetaan, THEN lähdeattribuutio ja hakuajankohta säilyvät.
- [ ] #4 GIVEN tuotantokeruuta arvioidaan, WHEN agentti tarkistaa specin, THEN compliance-, credential- ja rate limit -raja on eksplisiittinen.
- [ ] #5 GIVEN dataa käytetään käyttöliittymässä, WHEN spec luetaan, THEN se ei mahdollista sijoitusneuvontaa, suosituksia tai kaupankäyntipäätöksiä.
<!-- AC:END -->

## Definition of Done
<!-- DOD:BEGIN -->
- [ ] #1 Acceptance criteria on testattu tehtävän scopea vasten
- [ ] #2 Relevantit lint typecheck build ja testikomennot on ajettu tai rajaus on kirjattu
- [ ] #3 Salaisuuksia tokeneita credentialeja ja PII-tietoja ei palauteta lokiteta tai commitoida
- [ ] #4 Julkiset API data infra ja operointisopimukset on päivitetty tarvittaessa
- [ ] #5 Final Summary kuvaa toteutuksen tuloksen validoinnin ja rajaukset
<!-- DOD:END -->
