---
id: TASK-024
title: 'Notifications: Toimitustilan tarkastelu'
status: To Do
assignee: []
created_date: '2026-06-07 11:25'
labels:
  - Notifications
  - Backend
milestone: m-4
dependencies:
  - TASK-016
  - TASK-023
references:
  - >-
    .backlog/tasks/task-016 -
    Detail-spec-Notifications-messaging-and-delivery-contract.md
documentation:
  - .backlog/docs/intent/doc-001 - goal.md
  - .backlog/docs/specs/doc-006 - bounded-context-map-and-glossary.md
priority: medium
ordinal: 4000
---

## Description

<!-- SECTION:DESCRIPTION:BEGIN -->
### MITÄ
Toteuta Notifications-kontekstin käyttötapaus, jossa toimituspyynnön tai viestin toimitustila voidaan tarkastaa sisäisesti hyväksytyssä rajassa.

- Tarkastelu palauttaa toimituksen tilan ja olennaisen virheluokan.
- Tarkastelu ei palauta viestin salaisuuksia, credentialeja tai tarpeetonta PII:tä.
- Tuntematon toimitus käsitellään yhtenäisesti.

### MIKSI
Kutsuvat contextit ja testit tarvitsevat tavan todentaa, syntyikö viestitoimitus ja missä tilassa se on.
<!-- SECTION:DESCRIPTION:END -->

## Acceptance Criteria
<!-- AC:BEGIN -->
- [ ] #1 GIVEN toimitus on olemassa, WHEN toimitustilaa kysytään, THEN tila palautetaan detail-specin mukaisena summarynä.
- [ ] #2 GIVEN toimitusta ei löydy, WHEN toimitustilaa kysytään, THEN pyyntö hylätään tai palauttaa tyhjän tuloksen detail-specin mukaisesti ilman uuden toimituksen luontia.
- [ ] #3 GIVEN toimitus epäonnistui, WHEN tila palautetaan, THEN mukana on turvallinen virheluokka ilman raw-provider-virhettä.
- [ ] #4 GIVEN tila palautetaan tai lokitetaan, WHEN tulos muodostetaan, THEN salaisuuksia, credentialeja tai tarpeetonta PII:tä ei palauteta eikä lokiteta.
<!-- AC:END -->

## Definition of Done
<!-- DOD:BEGIN -->
- [ ] #1 Acceptance criteria on testattu tehtävän scopea vasten
- [ ] #2 Relevantit lint typecheck build ja testikomennot on ajettu tai rajaus on kirjattu
- [ ] #3 Salaisuuksia tokeneita credentialeja ja PII-tietoja ei palauteta lokiteta tai commitoida
- [ ] #4 Julkiset API data infra ja operointisopimukset on päivitetty tarvittaessa
- [ ] #5 Final Summary kuvaa toteutuksen tuloksen validoinnin ja rajaukset
<!-- DOD:END -->
