---
id: TASK-029
title: 'Companies: Päivitä yrityksen perustiedot mock-only YTJ-adapterilla'
status: To Do
assignee: []
created_date: '2026-06-07 11:26'
labels:
  - Companies
  - Backend
  - Integration
milestone: m-5
dependencies:
  - TASK-017
references:
  - .backlog/tasks/task-017 - Detail-spec-Companies-and-watchlist-contract.md
documentation:
  - .backlog/docs/intent/goal.md
  - .backlog/docs/specs/doc-006 - bounded-context-map-and-glossary.md
  - .backlog/docs/specs/doc-010 - external-data-source-compliance.md
priority: medium
ordinal: 5000
---

## Description

<!-- SECTION:DESCRIPTION:BEGIN -->
### MITÄ
Toteuta Companies and watchlist -kontekstin käyttötapaus, jossa seurattavan yrityksen perustiedot päivitetään mock-only YTJ-adapterin kautta.

- Adapteri ei tee tuotantokutsua YTJ:hin.
- Normalisoitu perustieto tallennetaan Companies/watchlist-kontekstin kielellä.
- Lähdeattribuutio säilyy.

### MIKSI
Yritysten perustietojen päivityspolku tarvitaan ennen tuotantointegraatiota, mutta YTJ:n tuotantokäyttö vaatii erillisen compliance-evidenssin.
<!-- SECTION:DESCRIPTION:END -->

## Acceptance Criteria
<!-- AC:BEGIN -->
- [ ] #1 GIVEN seurattava yritys on olemassa ja mock-only YTJ-vastaus on validi, WHEN perustiedot päivitetään, THEN normalisoidut perustiedot tallentuvat yritykselle.
- [ ] #2 GIVEN mock-vastaus on puutteellinen tai virheellinen, WHEN päivitystä käsitellään, THEN virhe käsitellään ilman yritysdatan korruptoitumista.
- [ ] #3 GIVEN YTJ-tuotantokutsu tai oikea credential tarvittaisiin, WHEN toteutusta arvioidaan, THEN tehtävä merkitään Blocked siltä osin eikä tuotantokutsua toteuteta.
- [ ] #4 GIVEN data tallennetaan, WHEN tietoa tarkastellaan myöhemmin, THEN lähde ja hakuajankohta ovat mukana.
- [ ] #5 GIVEN vastaus tai lokit muodostetaan, WHEN päivitys onnistuu tai epäonnistuu, THEN YTJ:n raw-mallia, credentialeja tai tarpeetonta PII:tä ei palauteta eikä lokiteta.
<!-- AC:END -->

## Definition of Done
<!-- DOD:BEGIN -->
- [ ] #1 Acceptance criteria on testattu tehtävän scopea vasten
- [ ] #2 Relevantit lint typecheck build ja testikomennot on ajettu tai rajaus on kirjattu
- [ ] #3 Salaisuuksia tokeneita credentialeja ja PII-tietoja ei palauteta lokiteta tai commitoida
- [ ] #4 Julkiset API data infra ja operointisopimukset on päivitetty tarvittaessa
- [ ] #5 Final Summary kuvaa toteutuksen tuloksen validoinnin ja rajaukset
<!-- DOD:END -->
