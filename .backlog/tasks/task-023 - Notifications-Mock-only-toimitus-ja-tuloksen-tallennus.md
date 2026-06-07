---
id: TASK-023
title: 'Notifications: Mock-only-toimitus ja tuloksen tallennus'
status: To Do
assignee: []
created_date: '2026-06-07 11:25'
labels:
  - Notifications
  - Backend
milestone: m-4
dependencies:
  - TASK-016
  - TASK-022
references:
  - >-
    .backlog/tasks/task-016 -
    Detail-spec-Notifications-messaging-and-delivery-contract.md
documentation:
  - .backlog/docs/intent/goal.md
  - .backlog/docs/specs/doc-006 - bounded-context-map-and-glossary.md
priority: medium
ordinal: 3000
---

## Description

<!-- SECTION:DESCRIPTION:BEGIN -->
### MITÄ
Toteuta Notifications-kontekstin käyttötapaus, jossa renderöity viesti toimitetaan mock-only-toimittajan kautta ja toimitustulos tallennetaan.

- Toimitus ei käytä oikeaa provideria tai credentialia.
- Onnistuminen ja epäonnistuminen tallennetaan tarkasteltavaksi.
- Virheet eivät paljasta salaisuuksia tai providerin raw-virheitä.

### MIKSI
Projektin alkuvaihe tarvitsee testattavan toimituspolun ilman tuotantolähetyksen riskiä tai provider-päätöstä.
<!-- SECTION:DESCRIPTION:END -->

## Acceptance Criteria
<!-- AC:BEGIN -->
- [ ] #1 GIVEN renderöity viesti ja mock-only-toimittaja, WHEN toimitus käynnistetään, THEN toimitusyritys kirjataan ja tulos tallennetaan.
- [ ] #2 GIVEN mock-toimitus epäonnistuu, WHEN tulos tallennetaan, THEN virheluokka tallentuu ilman salaisuuksia tai raw-provider-virhettä.
- [ ] #3 GIVEN oikeaa provideria tai credentialia tarvittaisiin, WHEN toteutusta arvioidaan, THEN tehtävä merkitään Blocked siltä osin eikä tuotantolähetystä toteuteta.
- [ ] #4 GIVEN toimitus onnistuu tai epäonnistuu, WHEN lokit muodostetaan, THEN viestin credentialeja tai tarpeetonta PII:tä ei lokiteta.
<!-- AC:END -->

## Definition of Done
<!-- DOD:BEGIN -->
- [ ] #1 Acceptance criteria on testattu tehtävän scopea vasten
- [ ] #2 Relevantit lint typecheck build ja testikomennot on ajettu tai rajaus on kirjattu
- [ ] #3 Salaisuuksia tokeneita credentialeja ja PII-tietoja ei palauteta lokiteta tai commitoida
- [ ] #4 Julkiset API data infra ja operointisopimukset on päivitetty tarvittaessa
- [ ] #5 Final Summary kuvaa toteutuksen tuloksen validoinnin ja rajaukset
<!-- DOD:END -->
