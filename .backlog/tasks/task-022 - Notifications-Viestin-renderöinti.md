---
id: TASK-022
title: 'Notifications: Viestin renderöinti'
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
  - .backlog/docs/intent/doc-001 - goal.md
  - .backlog/docs/specs/doc-006 - bounded-context-map-and-glossary.md
priority: medium
ordinal: 2000
---

## Description

<!-- SECTION:DESCRIPTION:BEGIN -->
### MITÄ
Toteuta Notifications-kontekstin käyttötapaus, jossa hyväksytty toimituspyyntö muutetaan lähetettäväksi viestisisällöksi.

- Renderöinti käyttää vain detail-specissä sallittuja viestipohjia ja muuttujia.
- Puuttuvat tai kielletyt muuttujat hylätään ennen toimitusta.
- Renderöity sisältö ei saa paljastaa credentialeja tai tarpeetonta PII:tä.

### MIKSI
Viestien muodostus pitää keskittää Notifications-kontekstiin, jotta kutsuvat contextit eivät rakenna toimituskanavakohtaista sisältöä.
<!-- SECTION:DESCRIPTION:END -->

## Acceptance Criteria
<!-- AC:BEGIN -->
- [ ] #1 GIVEN hyväksytty toimituspyyntö ja tarvittavat muuttujat, WHEN viesti renderöidään, THEN lähetettävä sisältö muodostuu detail-specin mukaisesti.
- [ ] #2 GIVEN viestipohja, muuttuja tai viestityyppi puuttuu, WHEN renderöintiä yritetään, THEN renderöinti hylätään eikä toimitusta synny.
- [ ] #3 GIVEN muuttuja sisältää credentialin tai tarpeetonta PII:tä, WHEN renderöintiä yritetään, THEN arvoa ei lisätä viestiin eikä lokiin.
- [ ] #4 GIVEN renderöinti onnistuu, WHEN tulos tallennetaan tai välitetään toimitukseen, THEN mukana on vain toimitukseen tarvittava sisältö.
<!-- AC:END -->

## Definition of Done
<!-- DOD:BEGIN -->
- [ ] #1 Acceptance criteria on testattu tehtävän scopea vasten
- [ ] #2 Relevantit lint typecheck build ja testikomennot on ajettu tai rajaus on kirjattu
- [ ] #3 Salaisuuksia tokeneita credentialeja ja PII-tietoja ei palauteta lokiteta tai commitoida
- [ ] #4 Julkiset API data infra ja operointisopimukset on päivitetty tarvittaessa
- [ ] #5 Final Summary kuvaa toteutuksen tuloksen validoinnin ja rajaukset
<!-- DOD:END -->
