---
id: TASK-014
title: 'Detail spec: data security config secrets ja operations guardrails'
status: To Do
assignee: []
created_date: '2026-06-07 11:22'
labels:
  - Project
  - Spec
  - Security
  - Infra
milestone: m-3
dependencies: []
documentation:
  - .backlog/docs/intent/goal.md
  - .backlog/docs/governance/Agenttien päätöksenteon reunaehdot.md
  - .backlog/docs/specs/doc-007 - security-data-classification.md
  - .backlog/docs/specs/doc-008 - config-secrets-catalog.md
  - .backlog/docs/specs/doc-009 - aws-runtime-operations.md
  - .backlog/docs/specs/doc-010 - external-data-source-compliance.md
priority: medium
ordinal: 1200
---

## Description

<!-- SECTION:DESCRIPTION:BEGIN -->
### MITÄ
Määritä projektin yhteiset data-, security-, config-, secrets- ja operations-guardrailit hyväksyttyjen korkean tason rajojen sisällä.

Specin tulee olla poikkileikkaava HOW-ohje, jota context-kohtaiset detail-specit täydentävät ilman päällekkäistä päätöstekstiä.

### MIKSI
Agentit tarvitsevat yhteisen turva- ja operointipohjan ennen tietomallien, adapterien, IAM-oikeuksien ja runtime-konfiguraation toteutusta.
<!-- SECTION:DESCRIPTION:END -->

## Acceptance Criteria
<!-- AC:BEGIN -->
- [ ] #1 GIVEN poikkileikkaava guardrail-spec tehdään, WHEN tehtävä valmistuu, THEN spec kuvaa data-, secret-, config-, logging-, IAM- ja deploy-rajat ilman context-kohtaisen mallin lukitsemista.
- [ ] #2 GIVEN context-kohtainen spec tarvitsee salaisuuden tai konfiguraation, WHEN se käyttää guardrailia, THEN se tietää mihin tieto kirjataan ja milloin pysähdytään.
- [ ] #3 GIVEN ulkoisen lähteen tuotantokäyttöä arvioidaan, WHEN spec luetaan, THEN mock-only ja compliance-evidenssin raja on yksiselitteinen.
- [ ] #4 GIVEN pysyvä kustannus-, security- tai deploy-vaikutus havaitaan, WHEN agentti arvioi ratkaisua, THEN se pysähtyy käyttäjän päätöstä varten.
<!-- AC:END -->

## Definition of Done
<!-- DOD:BEGIN -->
- [ ] #1 Acceptance criteria on testattu tehtävän scopea vasten
- [ ] #2 Relevantit lint typecheck build ja testikomennot on ajettu tai rajaus on kirjattu
- [ ] #3 Salaisuuksia tokeneita credentialeja ja PII-tietoja ei palauteta lokiteta tai commitoida
- [ ] #4 Julkiset API data infra ja operointisopimukset on päivitetty tarvittaessa
- [ ] #5 Final Summary kuvaa toteutuksen tuloksen validoinnin ja rajaukset
<!-- DOD:END -->
