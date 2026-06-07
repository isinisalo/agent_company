---
id: TASK-041
title: 'Scheduling: Retry tai failed-tila keruuajolle'
status: To Do
assignee: []
created_date: '2026-06-07 11:28'
labels:
  - Scheduling
  - Backend
  - Infra
milestone: m-8
dependencies:
  - TASK-020
  - TASK-040
references:
  - >-
    .backlog/tasks/task-020 -
    Detail-spec-Scheduling-event-schedule-retry-and-run-state-contract.md
documentation:
  - .backlog/docs/intent/doc-001 - goal.md
  - .backlog/docs/specs/doc-006 - bounded-context-map-and-glossary.md
  - .backlog/docs/specs/doc-009 - aws-runtime-operations.md
priority: medium
ordinal: 4000
---

## Description

<!-- SECTION:DESCRIPTION:BEGIN -->
### MITÄ
Toteuta Scheduling-kontekstin käyttötapaus, jossa epäonnistunut keruuajo merkitään uudelleenyritykseen tai lopullisesti epäonnistuneeksi.

- Retry noudattaa detail-specin yritysrajoja.
- Failed-tila säilyttää turvallisen virheluokan.
- Käsittely on idempotentti uudelleenajolle.

### MIKSI
Tausta-ajot epäonnistuvat ajoittain, ja järjestelmän pitää erottaa uudelleen yritettävät virheet lopullisista virheistä ilman datakorruptiota.
<!-- SECTION:DESCRIPTION:END -->

## Acceptance Criteria
<!-- AC:BEGIN -->
- [ ] #1 GIVEN keruuajo epäonnistui retry-kelpoisesti, WHEN retry arvioidaan, THEN ajo merkitään uudelleenyritykseen detail-specin rajojen mukaan.
- [ ] #2 GIVEN retry-raja on täyttynyt tai virhe ei ole retry-kelpoinen, WHEN retry arvioidaan, THEN ajo merkitään failed-tilaan.
- [ ] #3 GIVEN sama epäonnistumistulos käsitellään uudelleen, WHEN tila päivitetään, THEN käsittely on idempotentti.
- [ ] #4 GIVEN virhetila tallennetaan tai lokitetaan, WHEN tulos muodostetaan, THEN raw lähdevirhettä, credentialeja tai PII:tä ei paljasteta.
- [ ] #5 GIVEN retry voisi rikkoa ulkoisen lähteen kutsurajaa, WHEN retryä arvioidaan, THEN retry estetään tai viivästetään detail-specin mukaisesti.
<!-- AC:END -->

## Definition of Done
<!-- DOD:BEGIN -->
- [ ] #1 Acceptance criteria on testattu tehtävän scopea vasten
- [ ] #2 Relevantit lint typecheck build ja testikomennot on ajettu tai rajaus on kirjattu
- [ ] #3 Salaisuuksia tokeneita credentialeja ja PII-tietoja ei palauteta lokiteta tai commitoida
- [ ] #4 Julkiset API data infra ja operointisopimukset on päivitetty tarvittaessa
- [ ] #5 Final Summary kuvaa toteutuksen tuloksen validoinnin ja rajaukset
<!-- DOD:END -->
