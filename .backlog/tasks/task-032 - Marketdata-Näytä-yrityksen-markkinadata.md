---
id: TASK-032
title: 'Marketdata: Näytä yrityksen markkinadata'
status: To Do
assignee: []
created_date: '2026-06-07 11:26'
labels:
  - Marketdata
  - Backend
  - Frontend
milestone: m-6
dependencies:
  - TASK-018
  - TASK-031
references:
  - >-
    .backlog/tasks/task-018 -
    Detail-spec-Marketdata-collection-and-query-contract.md
documentation:
  - .backlog/docs/intent/goal.md
  - .backlog/docs/specs/doc-006 - bounded-context-map-and-glossary.md
priority: medium
ordinal: 3000
---

## Description

<!-- SECTION:DESCRIPTION:BEGIN -->
### MITÄ
Toteuta Marketdata-kontekstin käyttötapaus, jossa käyttäjä voi tarkastella seurattavan yrityksen tallennettua markkinadataa.

- Kysely palauttaa detail-specin mukaisen rajatun markkinadatasummaryn.
- Tulos sisältää lähdeattribuution käyttäjälle sopivassa muodossa.
- Tulos ei sisällä raw EODHD -mallia eikä credentialeja.

### MIKSI
Käyttäjän pitää nähdä seurattavan yrityksen markkinadata ilman, että palvelu antaa sijoitusneuvontaa tai paljastaa integraatiodetailit.
<!-- SECTION:DESCRIPTION:END -->

## Acceptance Criteria
<!-- AC:BEGIN -->
- [ ] #1 GIVEN yritykselle on tallennettua markkinadataa ja kutsuja on sallittu, WHEN dataa kysytään, THEN markkinadatasummary palautuu.
- [ ] #2 GIVEN yritykselle ei ole markkinadataa, WHEN dataa kysytään, THEN tyhjä tai puuttuva tulos palautuu detail-specin mukaisesti.
- [ ] #3 GIVEN kutsujalla ei ole oikeutta nähdä dataa, WHEN dataa kysytään, THEN toiminto hylätään ennen datan palautusta.
- [ ] #4 GIVEN tulos muodostetaan, WHEN se palautetaan, THEN mukana on lähdeattribuutio mutta ei raw EODHD -mallia tai credentialeja.
- [ ] #5 GIVEN dataa näytetään, WHEN käyttäjä tulkitsee tulosta, THEN vaste ei sisällä sijoitusneuvontaa, suositusta tai kaupankäyntipäätöstä.
<!-- AC:END -->

## Definition of Done
<!-- DOD:BEGIN -->
- [ ] #1 Acceptance criteria on testattu tehtävän scopea vasten
- [ ] #2 Relevantit lint typecheck build ja testikomennot on ajettu tai rajaus on kirjattu
- [ ] #3 Salaisuuksia tokeneita credentialeja ja PII-tietoja ei palauteta lokiteta tai commitoida
- [ ] #4 Julkiset API data infra ja operointisopimukset on päivitetty tarvittaessa
- [ ] #5 Final Summary kuvaa toteutuksen tuloksen validoinnin ja rajaukset
<!-- DOD:END -->
