---
id: TASK-035
title: 'Comments: Deduplikoi ja tallenna keskusteluaineisto'
status: To Do
assignee: []
created_date: '2026-06-07 11:27'
labels:
  - Comments
  - Backend
milestone: m-7
dependencies:
  - TASK-019
  - TASK-034
references:
  - >-
    .backlog/tasks/task-019 -
    Detail-spec-Comments-collection-and-query-contract.md
documentation:
  - .backlog/docs/intent/goal.md
  - .backlog/docs/specs/doc-006 - bounded-context-map-and-glossary.md
priority: medium
ordinal: 2000
---

## Description

<!-- SECTION:DESCRIPTION:BEGIN -->
### MITÄ
Toteuta Comments-kontekstin käyttötapaus, jossa normalisoitu keskusteluaineisto deduplikoidaan ja tallennetaan lähdeattribuution kanssa.

- Sama lähdekommentti ei synnytä hallitsemattomia duplikaatteja.
- Lähde, hakuajankohta ja lähteen tunniste säilyvät, kun ne ovat saatavilla.
- Tallennus ei käytä raw Inderes -mallia julkisena sopimuksena.

### MIKSI
Keskusteluaineistoa pitää voida päivittää toistuvasti ilman datan paisumista ja ilman lähdejäljitettävyyden katoamista.
<!-- SECTION:DESCRIPTION:END -->

## Acceptance Criteria
<!-- AC:BEGIN -->
- [ ] #1 GIVEN normalisoidut kommentit ja seurattava yritys, WHEN data tallennetaan, THEN kommentit ovat myöhemmin haettavissa yritykselle.
- [ ] #2 GIVEN sama lähdekommentti käsitellään uudelleen, WHEN tallennus suoritetaan, THEN hallitsematonta duplikaattia ei synny.
- [ ] #3 GIVEN kommentti puuttuu lähdeattribuutiosta, WHEN tallennusta yritetään, THEN tallennus hylätään tai attribuutio täydennetään detail-specin mukaan.
- [ ] #4 GIVEN data tallennetaan, WHEN julkista tai domain-mallia tarkastellaan, THEN raw Inderes -malli ei vuoda siihen.
- [ ] #5 GIVEN tallennus onnistuu tai epäonnistuu, WHEN lokit muodostetaan, THEN credentialeja, tarpeetonta PII:tä tai raw käyttäjäsisältöä ei lokiteta.
<!-- AC:END -->

## Definition of Done
<!-- DOD:BEGIN -->
- [ ] #1 Acceptance criteria on testattu tehtävän scopea vasten
- [ ] #2 Relevantit lint typecheck build ja testikomennot on ajettu tai rajaus on kirjattu
- [ ] #3 Salaisuuksia tokeneita credentialeja ja PII-tietoja ei palauteta lokiteta tai commitoida
- [ ] #4 Julkiset API data infra ja operointisopimukset on päivitetty tarvittaessa
- [ ] #5 Final Summary kuvaa toteutuksen tuloksen validoinnin ja rajaukset
<!-- DOD:END -->
