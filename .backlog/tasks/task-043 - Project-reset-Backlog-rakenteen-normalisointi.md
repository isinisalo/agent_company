---
id: TASK-043
title: 'Project reset: Backlog-rakenteen normalisointi'
status: Done
assignee: []
created_date: '2026-06-07 11:28'
updated_date: '2026-06-07 11:31'
labels:
  - Project
  - Governance
  - Backlog
milestone: m-2
dependencies: []
documentation:
  - .backlog/docs/intent/goal.md
  - .backlog/docs/governance/Agenttien päätöksenteon reunaehdot.md
  - .backlog/docs/specs/doc-006 - bounded-context-map-and-glossary.md
modified_files:
  - AGENTS.md
  - .backlog/docs/intent/goal.md
  - .backlog/docs/governance/Agenttien päätöksenteon reunaehdot.md
  - .backlog/docs/specs/doc-005 - project-structure-and-quality-gates.md
  - .backlog/docs/specs/doc-006 - bounded-context-map-and-glossary.md
  - .backlog/docs/specs/doc-007 - security-data-classification.md
  - .backlog/docs/specs/doc-008 - config-secrets-catalog.md
  - .backlog/docs/specs/doc-009 - aws-runtime-operations.md
  - .backlog/docs/specs/doc-010 - external-data-source-compliance.md
  - .backlog/decisions
  - .backlog/milestones
  - .backlog/tasks
  - .backlog/archive/tasks
priority: medium
ordinal: 1000
---

## Description

<!-- SECTION:DESCRIPTION:BEGIN -->
### MITÄ
Resetoi projektin Backlog-rakenne käyttäjän pyytämään malliin.

- Poista epäkanoniset decision-tiedostot.
- Arkistoi vanhat Auth detail-päätöstehtävät.
- Päivitä intent-, governance-, context map- ja guardrail-dokumentit.
- Luo Agent detail specifications -milestone ja bounded context -milestonet tehtävineen.
- Päivitä aktiiviset Auth use case -taskit käyttämään uutta Auth detail-spec -riippuvuutta.

### MIKSI
Käyttäjä määrittää GOAL/INTENT/WHY/WHAT-tason. Agentit määrittävät HOW-tason detail-spesifikaatioissa ja toteutustehtävissä ilman etukäteen lukittuja detail-ADR:iä.
<!-- SECTION:DESCRIPTION:END -->

## Acceptance Criteria
<!-- AC:BEGIN -->
- [x] #1 GIVEN reset valmistuu, WHEN Backlog tarkistetaan, THEN yksikään aktiivinen task ei viittaa poistettaviin Auth decision -tiedostoihin.
- [x] #2 GIVEN reset valmistuu, WHEN milestone-lista tarkistetaan, THEN Project reset, Agent detail specifications ja jokainen bounded context -milestone ovat olemassa.
- [x] #3 GIVEN reset valmistuu, WHEN dokumentit tarkistetaan, THEN goal, governance ja context map erottavat käyttäjän WHAT/WHY-tason agenttien HOW-tasosta.
- [x] #4 GIVEN reset valmistuu, WHEN decision-hakemisto tarkistetaan, THEN epäkanoniset ADR-tiedostot on poistettu.
- [x] #5 GIVEN reset valmistuu, WHEN validointi kirjataan, THEN puuttuvat sovelluskoodin tarkistuskomennot on dokumentoitu rajoituksena.
<!-- AC:END -->

## Final Summary

<!-- SECTION:FINAL_SUMMARY:BEGIN -->
Backlog-rakenne resetoitiin käyttäjän pyytämään malliin. Kaikki epäkanoniset decision-tiedostot poistettiin, vanhat Auth detail-päätöstehtävät arkistoitiin ja neutraloitiin, Auth use case -taskit päivitettiin riippumaan uudesta `TASK-015` Auth detail-specistä, ja uudet detail-spec- sekä bounded context -milestonet/taskit luotiin.

Validointi: `milestone_list` näyttää 8 milestonea (`Auth`, `Project reset`, `Agent detail specifications`, `Notifications`, `Companies and watchlist`, `Marketdata`, `Comments`, `Scheduling`). `find .backlog/decisions -maxdepth 1 -type f` ei palauta tiedostoja. Stale Auth-decision -viitehaku ei palauta osumia. `document_list` näyttää kanoniset `intent/goal.md` ja governance-polut.

Rajoitus: sovelluskoodia ei ole vielä (`backend/`, `frontend/`, `infra/` puuttuvat), joten backend/frontend/infra-lint-, typecheck-, build- tai testikomentoja ei voitu ajaa.
<!-- SECTION:FINAL_SUMMARY:END -->

## Definition of Done
<!-- DOD:BEGIN -->
- [x] #1 Acceptance criteria on testattu tehtävän scopea vasten
- [x] #2 Relevantit lint typecheck build ja testikomennot on ajettu tai rajaus on kirjattu
- [x] #3 Salaisuuksia tokeneita credentialeja ja PII-tietoja ei palauteta lokiteta tai commitoida
- [x] #4 Julkiset API data infra ja operointisopimukset on päivitetty tarvittaessa
- [x] #5 Final Summary kuvaa toteutuksen tuloksen validoinnin ja rajaukset
<!-- DOD:END -->
