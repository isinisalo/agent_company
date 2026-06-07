---
id: TASK-037
title: 'Comments: Seuraa keruun cursoria ja tilaa'
status: To Do
assignee: []
created_date: '2026-06-07 11:27'
labels:
  - Comments
  - Backend
  - Scheduling
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
  - .backlog/docs/specs/doc-010 - external-data-source-compliance.md
priority: medium
ordinal: 4000
---

## Description

<!-- SECTION:DESCRIPTION:BEGIN -->
### MITÄ
Toteuta Comments-kontekstin käyttötapaus, jossa keskustelukeruun cursor ja tila tallennetaan ja luetaan seuraavaa keruuta varten.

- Tila kertoo viimeisen tunnetun käsittelykohdan detail-specin mukaan.
- Epäonnistunut keruu ei saa siirtää cursoria virheellisesti.
- Tila ei sisällä credentialeja, raw käyttäjäsisältöä tai tarpeetonta PII:tä.

### MIKSI
Toistuva keruu tarvitsee jatkettavan tilan, jotta samaa aineistoa ei käsitellä hallitsemattomasti uudelleen eikä uutta aineistoa ohiteta.
<!-- SECTION:DESCRIPTION:END -->

## Acceptance Criteria
<!-- AC:BEGIN -->
- [ ] #1 GIVEN keruu onnistuu, WHEN cursor päivitetään, THEN seuraava keruu voi jatkaa detail-specin mukaisesta kohdasta.
- [ ] #2 GIVEN keruu epäonnistuu ennen turvallista checkpointia, WHEN tila tallennetaan, THEN cursor ei siirry virheellisesti eteenpäin.
- [ ] #3 GIVEN sama keruu käynnistyy uudelleen, WHEN cursoria käytetään, THEN käsittely on idempotentti detail-specin mukaan.
- [ ] #4 GIVEN tila palautetaan tai lokitetaan, WHEN tulos muodostetaan, THEN credentialeja, raw käyttäjäsisältöä tai tarpeetonta PII:tä ei palauteta eikä lokiteta.
- [ ] #5 GIVEN Inderes-tuotantokeruu olisi tarpeen, WHEN tilaa käytetään tuotantoon, THEN tehtävä pysyy mock-only-rajassa ilman hyväksyttyä compliance-evidenssiä.
<!-- AC:END -->

## Definition of Done
<!-- DOD:BEGIN -->
- [ ] #1 Acceptance criteria on testattu tehtävän scopea vasten
- [ ] #2 Relevantit lint typecheck build ja testikomennot on ajettu tai rajaus on kirjattu
- [ ] #3 Salaisuuksia tokeneita credentialeja ja PII-tietoja ei palauteta lokiteta tai commitoida
- [ ] #4 Julkiset API data infra ja operointisopimukset on päivitetty tarvittaessa
- [ ] #5 Final Summary kuvaa toteutuksen tuloksen validoinnin ja rajaukset
<!-- DOD:END -->
