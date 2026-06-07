---
id: TASK-039
title: 'Scheduling: Käynnistä erääntynyt keruuajo'
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
  - TASK-038
references:
  - >-
    .backlog/tasks/task-020 -
    Detail-spec-Scheduling-event-schedule-retry-and-run-state-contract.md
documentation:
  - .backlog/docs/intent/doc-001 - goal.md
  - .backlog/docs/specs/doc-006 - bounded-context-map-and-glossary.md
  - .backlog/docs/specs/doc-009 - aws-runtime-operations.md
priority: medium
ordinal: 2000
---

## Description

<!-- SECTION:DESCRIPTION:BEGIN -->
### MITÄ
Toteuta Scheduling-kontekstin käyttötapaus, jossa erääntynyt hyväksytty ajastus käynnistää keruuajon.

- Käynnistys välittää keräävälle contextille vain tarvittavan tunniste- ja kontekstitiedon.
- Scheduling ei päätä kerättävän datan domain-sääntöjä.
- Compliance-estetty tuotantokeruu ei käynnisty.

### MIKSI
Ajastusten pitää käynnistää Marketdata- ja Comments-keruut hallitusti ilman context-omistajuuden rikkomista.
<!-- SECTION:DESCRIPTION:END -->

## Acceptance Criteria
<!-- AC:BEGIN -->
- [ ] #1 GIVEN ajastus on erääntynyt ja sallittu, WHEN due-ajot käsitellään, THEN keruuajo käynnistyy detail-specin mukaisella payloadilla.
- [ ] #2 GIVEN ajastus ei ole erääntynyt, WHEN due-ajot käsitellään, THEN keruuta ei käynnistetä.
- [ ] #3 GIVEN lähteen tuotantokeruu on compliance-estetty, WHEN ajo olisi due, THEN tuotantoajo estetään ja tila kirjataan turvallisesti.
- [ ] #4 GIVEN käynnistys toistuu samalle ajolle, WHEN se käsitellään uudelleen, THEN käsittely on idempotentti detail-specin mukaan.
- [ ] #5 GIVEN payload tai lokit muodostetaan, WHEN ajo käynnistetään tai estetään, THEN salaisuuksia, credentialeja tai raw lähdedataa ei sisällytetä.
<!-- AC:END -->

## Definition of Done
<!-- DOD:BEGIN -->
- [ ] #1 Acceptance criteria on testattu tehtävän scopea vasten
- [ ] #2 Relevantit lint typecheck build ja testikomennot on ajettu tai rajaus on kirjattu
- [ ] #3 Salaisuuksia tokeneita credentialeja ja PII-tietoja ei palauteta lokiteta tai commitoida
- [ ] #4 Julkiset API data infra ja operointisopimukset on päivitetty tarvittaessa
- [ ] #5 Final Summary kuvaa toteutuksen tuloksen validoinnin ja rajaukset
<!-- DOD:END -->
