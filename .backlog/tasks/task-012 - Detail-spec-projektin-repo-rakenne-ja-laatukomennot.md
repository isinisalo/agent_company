---
id: TASK-012
title: 'Detail spec: projektin repo-rakenne ja laatukomennot'
status: To Do
assignee: []
created_date: '2026-06-07 11:22'
labels:
  - Project
  - Spec
milestone: m-3
dependencies: []
documentation:
  - .backlog/docs/intent/goal.md
  - .backlog/docs/governance/Agenttien päätöksenteon reunaehdot.md
  - .backlog/docs/specs/doc-005 - project-structure-and-quality-gates.md
priority: medium
ordinal: 1000
---

## Description

<!-- SECTION:DESCRIPTION:BEGIN -->
### MITÄ
Määritä projektin konkreettinen repo-skeleton ja sovellusalueiden validointikomennot hyväksyttyjen korkean tason rajojen sisällä.

Tehtävä tuottaa HOW-tason specin, jota myöhemmät backend-, frontend- ja infra-agentit käyttävät ilman, että käyttötapaustaskit joutuvat päättämään pakettirakennetta tai komentojen nimiä.

### MIKSI
Agentit tarvitsevat yhteisen toteutusrakenteen ja validointipinnan ennen sovelluskoodin lisäämistä.
<!-- SECTION:DESCRIPTION:END -->

## Acceptance Criteria
<!-- AC:BEGIN -->
- [ ] #1 GIVEN repo-rakenne määritetään, WHEN tehtävä valmistuu, THEN spec kuvaa sallitut backend-, frontend- ja infra-alihakemistot ilman uutta top-level sovellusaluetta.
- [ ] #2 GIVEN laatukomennot määritetään, WHEN tehtävä valmistuu, THEN spec nimeää backendin, frontendin ja infran kapeimmat validointikomennot tai dokumentoi puuttuvat komennot.
- [ ] #3 GIVEN spec hyväksytään tehtävän scopeen, WHEN myöhempi agentti toteuttaa sovelluskoodia, THEN se voi käyttää specin rakennetta ja komentoja ilman uutta repo-rakennepäätöstä.
- [ ] #4 GIVEN toteutus vaatisi uuden runtimeen, frameworkin tai top-level alueen, WHEN agentti arvioi muutosta, THEN tehtävä kirjataan Blocked eikä muutosta päätetä tässä specissä.
<!-- AC:END -->

## Definition of Done
<!-- DOD:BEGIN -->
- [ ] #1 Acceptance criteria on testattu tehtävän scopea vasten
- [ ] #2 Relevantit lint typecheck build ja testikomennot on ajettu tai rajaus on kirjattu
- [ ] #3 Salaisuuksia tokeneita credentialeja ja PII-tietoja ei palauteta lokiteta tai commitoida
- [ ] #4 Julkiset API data infra ja operointisopimukset on päivitetty tarvittaessa
- [ ] #5 Final Summary kuvaa toteutuksen tuloksen validoinnin ja rajaukset
<!-- DOD:END -->
