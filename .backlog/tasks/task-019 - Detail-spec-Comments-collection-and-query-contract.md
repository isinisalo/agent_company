---
id: TASK-019
title: 'Detail spec: Comments collection and query contract'
status: To Do
assignee: []
created_date: '2026-06-07 11:23'
updated_date: '2026-06-07 12:13'
labels:
  - Comments
  - Spec
  - Backend
milestone: m-3
dependencies:
  - TASK-017
documentation:
  - .backlog/docs/intent/doc-001 - goal.md
  - .backlog/docs/governance/Agenttien päätöksenteon reunaehdot.md
  - .backlog/docs/specs/doc-006 - bounded-context-map-and-glossary.md
  - .backlog/docs/specs/doc-010 - external-data-source-compliance.md
priority: medium
ordinal: 2400
---

## Description

<!-- SECTION:DESCRIPTION:BEGIN -->
### MITÄ
Määritä Comments bounded contextin HOW-tason keruu-, deduplikointi-, tallennus-, kysely-, Inderes-adapteri- ja testisopimus hyväksyttyjen projektirajojen sisällä.

Specin pitää tukea keskustelujen hakua, lähdeattribuutiota, cursor/state-käsittelyä, deduplikointia ja katselua mock-only-tilassa.

### MIKSI
Comments tuo keskusteluaineiston yritysnäkymään, mutta käyttäjäsisältöön, PII:hin ja Inderes-tuotantokeruuseen liittyy compliance-rajoja.
<!-- SECTION:DESCRIPTION:END -->

## Acceptance Criteria
<!-- AC:BEGIN -->
- [ ] #1 GIVEN Comments detail-spec tehdään, WHEN tehtävä valmistuu, THEN spec kuvaa keruun, deduplikoinnin, tallennuksen ja kyselyjen vastuut käyttötapausten kannalta riittävästi.
- [ ] #2 GIVEN Inderes-adapteria suunnitellaan, WHEN spec luetaan, THEN raw Inderes -malli ei vuoda domainiin tai julkiseen API:in.
- [ ] #3 GIVEN keskusteluaineisto tallennetaan, WHEN spec tarkistetaan, THEN lähdeattribuutio, hakuajankohta ja deduplikointiraja säilyvät.
- [ ] #4 GIVEN käyttäjäsisältöä tai PII:tä käsitellään, WHEN agentti tarkistaa specin, THEN käsittelyraja ja pysähtymissääntö ovat eksplisiittiset.
- [ ] #5 GIVEN tuotantokeruuta arvioidaan, WHEN agentti tarkistaa specin, THEN Inderes compliance -raja estää tuotantokutsun ilman hyväksyntää.
<!-- AC:END -->

## Definition of Done
<!-- DOD:BEGIN -->
- [ ] #1 Acceptance criteria on testattu tehtävän scopea vasten
- [ ] #2 Relevantit lint typecheck build ja testikomennot on ajettu tai rajaus on kirjattu
- [ ] #3 Salaisuuksia tokeneita credentialeja ja PII-tietoja ei palauteta lokiteta tai commitoida
- [ ] #4 Julkiset API data infra ja operointisopimukset on päivitetty tarvittaessa
- [ ] #5 Final Summary kuvaa toteutuksen tuloksen validoinnin ja rajaukset
<!-- DOD:END -->
