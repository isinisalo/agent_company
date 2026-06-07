---
id: TASK-036
title: 'Comments: Näytä yrityksen keskusteluaineisto'
status: To Do
assignee: []
created_date: '2026-06-07 11:27'
labels:
  - Comments
  - Backend
  - Frontend
milestone: m-7
dependencies:
  - TASK-019
  - TASK-035
references:
  - >-
    .backlog/tasks/task-019 -
    Detail-spec-Comments-collection-and-query-contract.md
documentation:
  - .backlog/docs/intent/doc-001 - goal.md
  - .backlog/docs/specs/doc-006 - bounded-context-map-and-glossary.md
priority: medium
ordinal: 3000
---

## Description

<!-- SECTION:DESCRIPTION:BEGIN -->
### MITÄ
Toteuta Comments-kontekstin käyttötapaus, jossa käyttäjä voi tarkastella seurattavan yrityksen tallennettua keskusteluaineistoa.

- Kysely palauttaa detail-specin mukaisen rajatun kommenttisummaryn.
- Tulos sisältää lähdeattribuution käyttäjälle sopivassa muodossa.
- Tulos ei sisällä raw Inderes -mallia, credentialeja tai tarpeetonta PII:tä.

### MIKSI
Käyttäjän pitää nähdä yritykseen liittyvä keskusteluaineisto ilman, että palvelu muuttuu yleiseksi sosiaalisen median keräimeksi tai paljastaa lähdemallin.
<!-- SECTION:DESCRIPTION:END -->

## Acceptance Criteria
<!-- AC:BEGIN -->
- [ ] #1 GIVEN yritykselle on tallennettuja kommentteja ja kutsuja on sallittu, WHEN kommentteja kysytään, THEN kommenttisummaryt palautuvat.
- [ ] #2 GIVEN yritykselle ei ole kommentteja, WHEN kommentteja kysytään, THEN tyhjä tai puuttuva tulos palautuu detail-specin mukaisesti.
- [ ] #3 GIVEN kutsujalla ei ole oikeutta nähdä dataa, WHEN kommentteja kysytään, THEN toiminto hylätään ennen datan palautusta.
- [ ] #4 GIVEN tulos muodostetaan, WHEN se palautetaan, THEN mukana on lähdeattribuutio mutta ei raw Inderes -mallia, credentialeja tai tarpeetonta PII:tä.
- [ ] #5 GIVEN kommentit sisältävät käyttäjäsisältöä, WHEN ne palautetaan tai lokitetaan, THEN käsittely noudattaa Comments detail-specin sanitointi- ja rajausehtoja.
<!-- AC:END -->

## Definition of Done
<!-- DOD:BEGIN -->
- [ ] #1 Acceptance criteria on testattu tehtävän scopea vasten
- [ ] #2 Relevantit lint typecheck build ja testikomennot on ajettu tai rajaus on kirjattu
- [ ] #3 Salaisuuksia tokeneita credentialeja ja PII-tietoja ei palauteta lokiteta tai commitoida
- [ ] #4 Julkiset API data infra ja operointisopimukset on päivitetty tarvittaessa
- [ ] #5 Final Summary kuvaa toteutuksen tuloksen validoinnin ja rajaukset
<!-- DOD:END -->
