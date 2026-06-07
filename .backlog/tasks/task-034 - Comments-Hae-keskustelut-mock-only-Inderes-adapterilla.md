---
id: TASK-034
title: 'Comments: Hae keskustelut mock-only Inderes-adapterilla'
status: To Do
assignee: []
created_date: '2026-06-07 11:27'
labels:
  - Comments
  - Backend
  - Integration
milestone: m-7
dependencies:
  - TASK-019
  - TASK-029
references:
  - >-
    .backlog/tasks/task-019 -
    Detail-spec-Comments-collection-and-query-contract.md
documentation:
  - .backlog/docs/intent/goal.md
  - .backlog/docs/specs/doc-006 - bounded-context-map-and-glossary.md
  - .backlog/docs/specs/doc-010 - external-data-source-compliance.md
priority: medium
ordinal: 1000
---

## Description

<!-- SECTION:DESCRIPTION:BEGIN -->
### MITÄ
Toteuta Comments-kontekstin käyttötapaus, jossa seurattavaan yritykseen liittyviä keskusteluja haetaan mock-only Inderes-adapterilla.

- Haku kohdistuu seurattavaan yritykseen.
- Adapteri ei tee tuotantokutsua Inderes Forumiin.
- Raw Inderes -malli normalisoidaan Comments-kontekstin kielelle.

### MIKSI
Keskusteluaineiston keruupolku tarvitaan ennen tuotantointegraatiota, mutta Inderes-tuotantokeruu on compliance-estetty.
<!-- SECTION:DESCRIPTION:END -->

## Acceptance Criteria
<!-- AC:BEGIN -->
- [ ] #1 GIVEN seurattava yritys ja validi mock-only Inderes-vastaus, WHEN keskustelut haetaan, THEN normalisoidut kommentit syntyvät tallennusta varten.
- [ ] #2 GIVEN yritys ei ole seurannassa, WHEN hakua yritetään, THEN haku hylätään eikä kommentteja synny.
- [ ] #3 GIVEN mock-vastaus on virheellinen, WHEN haku käsitellään, THEN virhe palautuu turvallisena virheluokkana ilman raw-lähdevirhettä.
- [ ] #4 GIVEN Inderes-tuotantokutsu tarvittaisiin, WHEN toteutusta arvioidaan, THEN tehtävä merkitään Blocked siltä osin eikä tuotantokutsua toteuteta.
- [ ] #5 GIVEN vastaus tai lokit muodostetaan, WHEN haku onnistuu tai epäonnistuu, THEN credentialeja, raw Inderes -mallia tai tarpeetonta PII:tä ei palauteta eikä lokiteta.
<!-- AC:END -->

## Definition of Done
<!-- DOD:BEGIN -->
- [ ] #1 Acceptance criteria on testattu tehtävän scopea vasten
- [ ] #2 Relevantit lint typecheck build ja testikomennot on ajettu tai rajaus on kirjattu
- [ ] #3 Salaisuuksia tokeneita credentialeja ja PII-tietoja ei palauteta lokiteta tai commitoida
- [ ] #4 Julkiset API data infra ja operointisopimukset on päivitetty tarvittaessa
- [ ] #5 Final Summary kuvaa toteutuksen tuloksen validoinnin ja rajaukset
<!-- DOD:END -->
