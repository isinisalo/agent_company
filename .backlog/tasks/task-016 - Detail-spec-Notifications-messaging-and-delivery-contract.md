---
id: TASK-016
title: 'Detail spec: Notifications messaging and delivery contract'
status: To Do
assignee: []
created_date: '2026-06-07 11:22'
updated_date: '2026-06-07 12:13'
labels:
  - Notifications
  - Spec
  - Backend
milestone: m-3
dependencies: []
documentation:
  - .backlog/docs/intent/doc-001 - goal.md
  - .backlog/docs/governance/Agenttien päätöksenteon reunaehdot.md
  - .backlog/docs/specs/doc-006 - bounded-context-map-and-glossary.md
priority: medium
ordinal: 2100
---

## Description

<!-- SECTION:DESCRIPTION:BEGIN -->
### MITÄ
Määritä Notifications bounded contextin HOW-tason viesti-, toimitus-, tila-, adapteri- ja testisopimus hyväksyttyjen projektirajojen sisällä.

Specin pitää tukea toimituspyynnön vastaanottoa, viestin renderöintiä, mock-only-toimitusta, toimitustuloksen tallennusta ja sisäistä toimitustilan tarkastelua.

### MIKSI
Auth ja muut contextit tarvitsevat ilmoituskyvykkyyden ilman, että ne päättävät Notifications-kontekstin toimituskanavaa tai tuotantolähetyksen ehtoja.
<!-- SECTION:DESCRIPTION:END -->

## Acceptance Criteria
<!-- AC:BEGIN -->
- [ ] #1 GIVEN Notifications detail-spec tehdään, WHEN tehtävä valmistuu, THEN spec kuvaa toimituspyynnön, viestin renderöinnin ja toimitustilan vastuut.
- [ ] #2 GIVEN tuotantolähetystä arvioidaan, WHEN spec luetaan, THEN agentti tietää, että provider, lähettäjä, credentialit ja tuotantolähetys ovat erillisen hyväksynnän takana.
- [ ] #3 GIVEN Auth tai muu context pyytää viestiä, WHEN spec luetaan, THEN plaintext-salaisuuksien ja PII:n käsittelyraja on eksplisiittinen.
- [ ] #4 GIVEN mock-only-toimitus toteutetaan, WHEN spec tarkistetaan, THEN se on testattavissa ilman oikeaa provideria tai credentialia.
<!-- AC:END -->

## Definition of Done
<!-- DOD:BEGIN -->
- [ ] #1 Acceptance criteria on testattu tehtävän scopea vasten
- [ ] #2 Relevantit lint typecheck build ja testikomennot on ajettu tai rajaus on kirjattu
- [ ] #3 Salaisuuksia tokeneita credentialeja ja PII-tietoja ei palauteta lokiteta tai commitoida
- [ ] #4 Julkiset API data infra ja operointisopimukset on päivitetty tarvittaessa
- [ ] #5 Final Summary kuvaa toteutuksen tuloksen validoinnin ja rajaukset
<!-- DOD:END -->
