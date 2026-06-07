---
id: TASK-015
title: 'Detail spec: Auth domain API ja persistence contract'
status: To Do
assignee: []
created_date: '2026-06-07 11:22'
updated_date: '2026-06-07 12:19'
labels:
  - Auth
  - Spec
  - Backend
milestone: m-3
dependencies:
  - TASK-013
documentation:
  - .backlog/docs/intent/doc-001 - goal.md
  - .backlog/docs/specs/doc-006 - bounded-context-map-and-glossary.md
  - .backlog/docs/specs/doc-007 - security-data-classification.md
priority: medium
ordinal: 2000
---

## Description

<!-- SECTION:DESCRIPTION:BEGIN -->
### MITÄ
Määritä Auth bounded contextin HOW-tason domain-, API-, persistence-, security- ja testisopimus hyväksyttyjen projektirajojen sisällä.

Specin pitää tukea rekisteröintiä, kirjautumista, sähköpostivahvistusta, salasanan resetointia, käyttäjien listausta sekä enable-, disable- ja delete-käyttötapauksia ilman uutta ADR:ää.

### MIKSI
Auth use case -taskit tarvitsevat yhteisen toteutussopimuksen, mutta käyttäjä ei halua lukita detail-ratkaisuja etukäteen ADR-päätöksinä.
<!-- SECTION:DESCRIPTION:END -->

## Acceptance Criteria
<!-- AC:BEGIN -->
- [ ] #1 GIVEN Auth detail-spec tehdään, WHEN tehtävä valmistuu, THEN spec kuvaa Authin domain-kielen, tilat ja invarianssit käyttötapausten kannalta riittävästi.
- [ ] #2 GIVEN Auth API suunnitellaan, WHEN tehtävä valmistuu, THEN spec kuvaa julkiset ja admin-rajat, request/response-periaatteet, virheet ja authz-säännöt ilman credentialien vuotoa.
- [ ] #3 GIVEN Auth persistence suunnitellaan, WHEN tehtävä valmistuu, THEN spec kuvaa tarvittavat access patternit ja salaisuuksien tallennusrajat ilman tauluskannaukseen perustuvaa normaalia liikennettä.
- [ ] #4 GIVEN Auth käsittelee salasanoja, tokeneita tai PII:tä, WHEN spec tarkistetaan, THEN plaintext-arvojen, digestien, JWT:ien ja PII:n vuotamattomuus on eksplisiittinen.
- [ ] #5 GIVEN jokin Auth-ratkaisu vaatisi uuden autentikointimallin, tuotantocredentialin tai cross-context deletion -politiikan, WHEN agentti arvioi sitä, THEN se pysähtyy eikä lukitse ratkaisua tässä tehtävässä.
<!-- AC:END -->

## Definition of Done
<!-- DOD:BEGIN -->
- [ ] #1 Acceptance criteria on testattu tehtävän scopea vasten
- [ ] #2 Relevantit lint typecheck build ja testikomennot on ajettu tai rajaus on kirjattu
- [ ] #3 Salaisuuksia tokeneita credentialeja ja PII-tietoja ei palauteta lokiteta tai commitoida
- [ ] #4 Julkiset API data infra ja operointisopimukset on päivitetty tarvittaessa
- [ ] #5 Final Summary kuvaa toteutuksen tuloksen validoinnin ja rajaukset
<!-- DOD:END -->
