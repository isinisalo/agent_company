---
id: TASK-040
title: 'Scheduling: Tallenna keruuajon tulos'
status: To Do
assignee: []
created_date: '2026-06-07 11:27'
labels:
  - Scheduling
  - Backend
milestone: m-8
dependencies:
  - TASK-020
  - TASK-039
references:
  - >-
    .backlog/tasks/task-020 -
    Detail-spec-Scheduling-event-schedule-retry-and-run-state-contract.md
documentation:
  - .backlog/docs/intent/doc-001 - goal.md
  - .backlog/docs/specs/doc-006 - bounded-context-map-and-glossary.md
priority: medium
ordinal: 3000
---

## Description

<!-- SECTION:DESCRIPTION:BEGIN -->
### MITÄ
Toteuta Scheduling-kontekstin käyttötapaus, jossa keruuajon tulos tallennetaan ajon seurantaa varten.

- Tulos kertoo onnistuiko, epäonnistuiko vai estettiinkö ajo.
- Tulos ei omista kerätyn datan sisältöä.
- Tulos ei sisällä salaisuuksia, credentialeja tai raw lähdedataa.

### MIKSI
Ajastusten seurantaan tarvitaan tieto siitä, mitä ajoille tapahtui ja voidaanko niitä yrittää uudelleen.
<!-- SECTION:DESCRIPTION:END -->

## Acceptance Criteria
<!-- AC:BEGIN -->
- [ ] #1 GIVEN keruuajo onnistuu, WHEN tulos tallennetaan, THEN ajon tila merkitään onnistuneeksi detail-specin mukaan.
- [ ] #2 GIVEN keruuajo epäonnistuu, WHEN tulos tallennetaan, THEN ajon tila ja turvallinen virheluokka tallentuvat.
- [ ] #3 GIVEN keruuajo estetään compliance-rajan vuoksi, WHEN tulos tallennetaan, THEN esto näkyy erillisenä turvallisena tilana.
- [ ] #4 GIVEN kerätty data kuuluu Marketdata- tai Comments-kontekstille, WHEN run-tulos tallennetaan, THEN Scheduling ei tallenna kerätyn datan sisältöä.
- [ ] #5 GIVEN tulos palautetaan tai lokitetaan, WHEN se muodostetaan, THEN salaisuuksia, credentialeja tai raw lähdedataa ei palauteta eikä lokiteta.
<!-- AC:END -->

## Definition of Done
<!-- DOD:BEGIN -->
- [ ] #1 Acceptance criteria on testattu tehtävän scopea vasten
- [ ] #2 Relevantit lint typecheck build ja testikomennot on ajettu tai rajaus on kirjattu
- [ ] #3 Salaisuuksia tokeneita credentialeja ja PII-tietoja ei palauteta lokiteta tai commitoida
- [ ] #4 Julkiset API data infra ja operointisopimukset on päivitetty tarvittaessa
- [ ] #5 Final Summary kuvaa toteutuksen tuloksen validoinnin ja rajaukset
<!-- DOD:END -->
