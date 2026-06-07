---
id: TASK-042
title: 'Scheduling: Estä compliance-puutteinen tuotantokeruu'
status: To Do
assignee: []
created_date: '2026-06-07 11:28'
labels:
  - Scheduling
  - Backend
  - Compliance
milestone: m-8
dependencies:
  - TASK-020
  - TASK-038
references:
  - >-
    .backlog/tasks/task-020 -
    Detail-spec-Scheduling-event-schedule-retry-and-run-state-contract.md
documentation:
  - .backlog/docs/intent/goal.md
  - .backlog/docs/specs/doc-006 - bounded-context-map-and-glossary.md
  - .backlog/docs/specs/doc-010 - external-data-source-compliance.md
priority: medium
ordinal: 5000
---

## Description

<!-- SECTION:DESCRIPTION:BEGIN -->
### MITÄ
Toteuta Scheduling-kontekstin turvakäyttötapaus, joka estää tuotantokeruun ulkoisesta lähteestä, kun compliance-evidenssi puuttuu.

- Esto koskee EODHD-, YTJ- ja Inderes-tuotantokeruita.
- Mock-only- ja testipolut voivat toimia detail-specin mukaan.
- Esto kirjataan turvallisesti ilman credentialeja tai raw lähdedataa.

### MIKSI
Projektin ulkoiset lähteet eivät saa käynnistyä tuotannossa ennen käyttöehtojen, lisenssin, lähdemaininnan, kutsurajan ja credential-käsittelyn hyväksyntää.
<!-- SECTION:DESCRIPTION:END -->

## Acceptance Criteria
<!-- AC:BEGIN -->
- [ ] #1 GIVEN lähteeltä puuttuu hyväksytty compliance-evidenssi, WHEN tuotantokeruu olisi käynnistymässä, THEN Scheduling estää ajon.
- [ ] #2 GIVEN mock-only-ajo on sallittu, WHEN ajo käynnistetään testipolussa, THEN se saa jatkua ilman tuotantocredentialia.
- [ ] #3 GIVEN tuotantokeruu estetään, WHEN run-tulos tallennetaan, THEN eston syy tallentuu turvallisena tilana.
- [ ] #4 GIVEN eston lokit muodostetaan, WHEN lokit tarkistetaan, THEN niissä ei ole API-avaimia, tokeneita, credentialeja tai raw lähdedataa.
- [ ] #5 GIVEN compliance-evidenssi on myöhemmin hyväksytty, WHEN tuotantokeruuta arvioidaan, THEN uusi tehtävä tai spec päättää tuotantopolun aktivoinnin erikseen.
<!-- AC:END -->

## Definition of Done
<!-- DOD:BEGIN -->
- [ ] #1 Acceptance criteria on testattu tehtävän scopea vasten
- [ ] #2 Relevantit lint typecheck build ja testikomennot on ajettu tai rajaus on kirjattu
- [ ] #3 Salaisuuksia tokeneita credentialeja ja PII-tietoja ei palauteta lokiteta tai commitoida
- [ ] #4 Julkiset API data infra ja operointisopimukset on päivitetty tarvittaessa
- [ ] #5 Final Summary kuvaa toteutuksen tuloksen validoinnin ja rajaukset
<!-- DOD:END -->
