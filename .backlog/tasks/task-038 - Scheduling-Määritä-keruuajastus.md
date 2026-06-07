---
id: TASK-038
title: 'Scheduling: Määritä keruuajastus'
status: To Do
assignee: []
created_date: '2026-06-07 11:27'
labels:
  - Scheduling
  - Backend
  - Infra
milestone: m-8
dependencies:
  - TASK-020
references:
  - >-
    .backlog/tasks/task-020 -
    Detail-spec-Scheduling-event-schedule-retry-and-run-state-contract.md
documentation:
  - .backlog/docs/intent/doc-001 - goal.md
  - .backlog/docs/specs/doc-006 - bounded-context-map-and-glossary.md
  - .backlog/docs/specs/doc-009 - aws-runtime-operations.md
priority: medium
ordinal: 1000
---

## Description

<!-- SECTION:DESCRIPTION:BEGIN -->
### MITÄ
Toteuta Scheduling-kontekstin käyttötapaus, jossa ylläpitäjä määrittää hyväksytyn keruuajastuksen.

- Ajastus koskee detail-specissä sallittua keruutyyppiä ja kohdetta.
- Ajastus ei käynnistä tuotantokeruuta, jos lähteen compliance on estetty.
- Virheellinen tai liian aggressiivinen ajastus hylätään.

### MIKSI
Keruiden pitää olla toistettavia ja hallittuja ilman, että agentti arvaa ulkoisten lähteiden kutsurajoja.
<!-- SECTION:DESCRIPTION:END -->

## Acceptance Criteria
<!-- AC:BEGIN -->
- [ ] #1 GIVEN hallintakäyttäjä antaa validin ajastuksen sallitulle keruulle, WHEN ajastus tallennetaan, THEN se on käytettävissä due-ajojen laskentaan.
- [ ] #2 GIVEN ajastus koskee compliance-estettyä tuotantokeruuta, WHEN ajastusta käsitellään, THEN tuotantoajo estetään tai merkitään mock-only-rajatuksi detail-specin mukaan.
- [ ] #3 GIVEN ajastus on puutteellinen, virheellinen tai kutsurajoihin nähden liian aggressiivinen, WHEN sitä käsitellään, THEN ajastus hylätään.
- [ ] #4 GIVEN kutsuja ei ole hallintakäyttäjä, WHEN ajastusta yritetään määrittää, THEN toiminto hylätään ennen muutosta.
- [ ] #5 GIVEN ajastus tallennetaan tai hylätään, WHEN lokit muodostetaan, THEN salaisuuksia, credentialeja tai tuotantolähteiden raw-tietoja ei lokiteta.
<!-- AC:END -->

## Definition of Done
<!-- DOD:BEGIN -->
- [ ] #1 Acceptance criteria on testattu tehtävän scopea vasten
- [ ] #2 Relevantit lint typecheck build ja testikomennot on ajettu tai rajaus on kirjattu
- [ ] #3 Salaisuuksia tokeneita credentialeja ja PII-tietoja ei palauteta lokiteta tai commitoida
- [ ] #4 Julkiset API data infra ja operointisopimukset on päivitetty tarvittaessa
- [ ] #5 Final Summary kuvaa toteutuksen tuloksen validoinnin ja rajaukset
<!-- DOD:END -->
