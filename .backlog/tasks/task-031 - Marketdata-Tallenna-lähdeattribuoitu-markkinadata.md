---
id: TASK-031
title: 'Marketdata: Tallenna lähdeattribuoitu markkinadata'
status: To Do
assignee: []
created_date: '2026-06-07 11:26'
labels:
  - Marketdata
  - Backend
milestone: m-6
dependencies:
  - TASK-018
  - TASK-030
references:
  - >-
    .backlog/tasks/task-018 -
    Detail-spec-Marketdata-collection-and-query-contract.md
documentation:
  - .backlog/docs/intent/goal.md
  - .backlog/docs/specs/doc-006 - bounded-context-map-and-glossary.md
priority: medium
ordinal: 2000
---

## Description

<!-- SECTION:DESCRIPTION:BEGIN -->
### MITÄ
Toteuta Marketdata-kontekstin käyttötapaus, jossa normalisoitu markkinadata tallennetaan lähdeattribuution kanssa.

- Tallennus kohdistuu seurattavaan yritykseen.
- Lähde, hakuajankohta ja detail-specissä määritetyt tunnisteet säilyvät.
- Tallennus ei käytä raw EODHD -mallia julkisena sopimuksena.

### MIKSI
Käyttäjälle näytettävän markkinadatan pitää olla jäljitettävää lähteeseen ja hakuhetkeen.
<!-- SECTION:DESCRIPTION:END -->

## Acceptance Criteria
<!-- AC:BEGIN -->
- [ ] #1 GIVEN normalisoitu markkinadata ja seurattava yritys, WHEN data tallennetaan, THEN se on myöhemmin haettavissa yritykselle.
- [ ] #2 GIVEN tallennettava data puuttuu lähdeattribuutiosta, WHEN tallennusta yritetään, THEN tallennus hylätään tai attribuutio täydennetään detail-specin mukaan.
- [ ] #3 GIVEN sama lähdedata käsitellään uudelleen, WHEN tallennus suoritetaan, THEN data ei korruptoidu eikä hallitsematonta duplikaattia synny.
- [ ] #4 GIVEN data tallennetaan, WHEN julkista tai domain-mallia tarkastellaan, THEN raw EODHD -malli ei vuoda siihen.
- [ ] #5 GIVEN tallennus onnistuu tai epäonnistuu, WHEN lokit muodostetaan, THEN credentialeja tai raw lähdedataa ei lokiteta.
<!-- AC:END -->

## Definition of Done
<!-- DOD:BEGIN -->
- [ ] #1 Acceptance criteria on testattu tehtävän scopea vasten
- [ ] #2 Relevantit lint typecheck build ja testikomennot on ajettu tai rajaus on kirjattu
- [ ] #3 Salaisuuksia tokeneita credentialeja ja PII-tietoja ei palauteta lokiteta tai commitoida
- [ ] #4 Julkiset API data infra ja operointisopimukset on päivitetty tarvittaessa
- [ ] #5 Final Summary kuvaa toteutuksen tuloksen validoinnin ja rajaukset
<!-- DOD:END -->
