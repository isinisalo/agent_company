---
id: TASK-021
title: 'Notifications: Toimituspyynnön vastaanotto'
status: To Do
assignee: []
created_date: '2026-06-07 11:25'
labels:
  - Notifications
  - Backend
milestone: m-4
dependencies:
  - TASK-016
references:
  - >-
    .backlog/tasks/task-016 -
    Detail-spec-Notifications-messaging-and-delivery-contract.md
documentation:
  - .backlog/docs/intent/goal.md
  - .backlog/docs/specs/doc-006 - bounded-context-map-and-glossary.md
priority: medium
ordinal: 1000
---

## Description

<!-- SECTION:DESCRIPTION:BEGIN -->
### MITÄ
Toteuta Notifications-kontekstin käyttötapaus, jossa toinen context voi pyytää käyttäjälle lähetettävää viestiä.

- Toimituspyyntö hyväksyy vain detail-specissä sallitut viestityypit ja vastaanottajatiedot.
- Pyyntö ei saa sisältää tarpeettomia salaisuuksia tai credentialeja.
- Hyväksytty pyyntö kirjataan toimitettavaksi tai hylätään validointivirheenä.

### MIKSI
Auth ja muut contextit tarvitsevat yhteisen tavan pyytää käyttäjäviestejä ilman, että ne päättävät viestikanavan toteutusta.
<!-- SECTION:DESCRIPTION:END -->

## Acceptance Criteria
<!-- AC:BEGIN -->
- [ ] #1 GIVEN validi toimituspyyntö sallitulle viestityypille, WHEN pyyntö käsitellään, THEN se hyväksytään toimitettavaksi.
- [ ] #2 GIVEN toimituspyyntö on puutteellinen, tuntematon tai kiellettyä tyyppiä, WHEN pyyntö käsitellään, THEN se hylätään eikä toimitusta synny.
- [ ] #3 GIVEN toimituspyyntö sisältää tarpeetonta PII:tä, credentialeja tai salaisuuksia, WHEN pyyntö käsitellään, THEN se hylätään tai sanitisoidaan Notifications detail-specin mukaan.
- [ ] #4 GIVEN pyyntö hyväksytään tai hylätään, WHEN vastaus ja lokit muodostetaan, THEN salaisuuksia tai credentialeja ei palauteta eikä lokiteta.
<!-- AC:END -->

## Definition of Done
<!-- DOD:BEGIN -->
- [ ] #1 Acceptance criteria on testattu tehtävän scopea vasten
- [ ] #2 Relevantit lint typecheck build ja testikomennot on ajettu tai rajaus on kirjattu
- [ ] #3 Salaisuuksia tokeneita credentialeja ja PII-tietoja ei palauteta lokiteta tai commitoida
- [ ] #4 Julkiset API data infra ja operointisopimukset on päivitetty tarvittaessa
- [ ] #5 Final Summary kuvaa toteutuksen tuloksen validoinnin ja rajaukset
<!-- DOD:END -->
