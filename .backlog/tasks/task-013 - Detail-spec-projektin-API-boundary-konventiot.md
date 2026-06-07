---
id: TASK-013
title: 'Detail spec: projektin API boundary -konventiot'
status: To Do
assignee: []
created_date: '2026-06-07 11:22'
labels:
  - Project
  - Spec
  - API
milestone: m-3
dependencies: []
documentation:
  - .backlog/docs/intent/doc-001 - goal.md
  - .backlog/docs/governance/Agenttien päätöksenteon reunaehdot.md
  - .backlog/docs/specs/doc-006 - bounded-context-map-and-glossary.md
priority: medium
ordinal: 1100
---

## Description

<!-- SECTION:DESCRIPTION:BEGIN -->
### MITÄ
Määritä julkisen backend API:n yhteiset boundary-konventiot hyväksyttyjen korkean tason rajojen sisällä.

Specin tulee ohjata versiointia, authn/authz-rajaa, virhevastauksia, CORS-vaikutusten arviointia ja raw-mallien vuotamattomuutta ilman context-kohtaisten endpointtien lukitsemista.

### MIKSI
Context-kohtaiset API-taskit tarvitsevat yhteiset rajat, jotta ne eivät toista tai ristiriitaisesti päätä API-perusmallia.
<!-- SECTION:DESCRIPTION:END -->

## Acceptance Criteria
<!-- AC:BEGIN -->
- [ ] #1 GIVEN API boundary -konventiot määritetään, WHEN tehtävä valmistuu, THEN spec erottaa yhteiset API-säännöt context-kohtaisista endpoint-sopimuksista.
- [ ] #2 GIVEN autentikoitu API-kutsu suunnitellaan, WHEN spec luetaan, THEN agentti tietää miten principal, bearer-token ja use case -raja erotetaan toisistaan.
- [ ] #3 GIVEN API-virhe suunnitellaan, WHEN spec luetaan, THEN agentti tietää mitä ei saa paljastaa käyttäjälle tai lokiin.
- [ ] #4 GIVEN endpoint muuttaisi julkista sopimusta pysyvästi, WHEN agentti arvioi muutosta, THEN muutos tehdään vain sitä koskevassa taskissa tai specissä.
<!-- AC:END -->

## Definition of Done
<!-- DOD:BEGIN -->
- [ ] #1 Acceptance criteria on testattu tehtävän scopea vasten
- [ ] #2 Relevantit lint typecheck build ja testikomennot on ajettu tai rajaus on kirjattu
- [ ] #3 Salaisuuksia tokeneita credentialeja ja PII-tietoja ei palauteta lokiteta tai commitoida
- [ ] #4 Julkiset API data infra ja operointisopimukset on päivitetty tarvittaessa
- [ ] #5 Final Summary kuvaa toteutuksen tuloksen validoinnin ja rajaukset
<!-- DOD:END -->
