---
id: TASK-020
title: 'Detail spec: Scheduling event schedule retry and run-state contract'
status: To Do
assignee: []
created_date: '2026-06-07 11:23'
labels:
  - Scheduling
  - Spec
  - Backend
  - Infra
milestone: m-3
dependencies:
  - TASK-014
  - TASK-018
  - TASK-019
documentation:
  - .backlog/docs/intent/doc-001 - goal.md
  - .backlog/docs/governance/Agenttien päätöksenteon reunaehdot.md
  - .backlog/docs/specs/doc-006 - bounded-context-map-and-glossary.md
  - .backlog/docs/specs/doc-009 - aws-runtime-operations.md
  - .backlog/docs/specs/doc-010 - external-data-source-compliance.md
priority: medium
ordinal: 2500
---

## Description

<!-- SECTION:DESCRIPTION:BEGIN -->
### MITÄ
Määritä Scheduling bounded contextin HOW-tason event-, schedule-, retry-, idempotenssi-, run-state- ja testisopimus hyväksyttyjen projektirajojen sisällä.

Specin pitää tukea keruuajastusten määrittelyä, due-ajojen käynnistämistä, run-tuloksen tallennusta, retry/failed-tiloja ja tuotantokeruun compliance-estoa.

### MIKSI
Ajastukset käynnistävät muita contexteja mutta eivät saa omia niiden datan domain-sääntöjä tai ohittaa lähdekohtaisia tuotantorajoja.
<!-- SECTION:DESCRIPTION:END -->

## Acceptance Criteria
<!-- AC:BEGIN -->
- [ ] #1 GIVEN Scheduling detail-spec tehdään, WHEN tehtävä valmistuu, THEN spec kuvaa schedule-, trigger-, run-state-, retry- ja idempotenssirajat käyttötapausten kannalta riittävästi.
- [ ] #2 GIVEN Scheduling käynnistää Marketdata- tai Comments-keruun, WHEN spec luetaan, THEN kerättävän datan domain-säännöt pysyvät keräävällä contextilla.
- [ ] #3 GIVEN ulkoisen lähteen tuotantokeruu on compliance-estetty, WHEN schedule arvioidaan, THEN spec estää tuotantoajon mutta sallii mock/test-polun.
- [ ] #4 GIVEN tausta-ajo epäonnistuu, WHEN spec luetaan, THEN agentti tietää miten epäonnistuminen kirjataan ilman credentialien tai PII:n vuotoa.
<!-- AC:END -->

## Definition of Done
<!-- DOD:BEGIN -->
- [ ] #1 Acceptance criteria on testattu tehtävän scopea vasten
- [ ] #2 Relevantit lint typecheck build ja testikomennot on ajettu tai rajaus on kirjattu
- [ ] #3 Salaisuuksia tokeneita credentialeja ja PII-tietoja ei palauteta lokiteta tai commitoida
- [ ] #4 Julkiset API data infra ja operointisopimukset on päivitetty tarvittaessa
- [ ] #5 Final Summary kuvaa toteutuksen tuloksen validoinnin ja rajaukset
<!-- DOD:END -->
