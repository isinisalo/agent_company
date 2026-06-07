---
id: TASK-033
title: 'Marketdata: Käsittele lähdevirhe ja kutsuraja'
status: To Do
assignee: []
created_date: '2026-06-07 11:26'
labels:
  - Marketdata
  - Backend
  - Integration
milestone: m-6
dependencies:
  - TASK-018
  - TASK-030
references:
  - >-
    .backlog/tasks/task-018 -
    Detail-spec-Marketdata-collection-and-query-contract.md
documentation:
  - .backlog/docs/intent/doc-001 - goal.md
  - .backlog/docs/specs/doc-006 - bounded-context-map-and-glossary.md
  - .backlog/docs/specs/doc-010 - external-data-source-compliance.md
priority: medium
ordinal: 4000
---

## Description

<!-- SECTION:DESCRIPTION:BEGIN -->
### MITÄ
Toteuta Marketdata-kontekstin käyttötapaus, jossa EODHD-adapterin virhe, timeout tai kutsuraja käsitellään turvallisesti.

- Virhe kirjataan Marketdata-kontekstin turvallisena virheluokkana.
- Raw-lähdevirhe, API-avain tai credential ei vuoda vastaukseen tai lokiin.
- Uudelleenyrityksen tai epäonnistumisen raja noudattaa detail-speciä.

### MIKSI
Integraatiovirheet eivät saa korruptoida dataa, rikkoa kutsurajoja tai paljastaa ulkoisen palvelun sisäisiä tietoja.
<!-- SECTION:DESCRIPTION:END -->

## Acceptance Criteria
<!-- AC:BEGIN -->
- [ ] #1 GIVEN mock-only EODHD-adapteri palauttaa timeoutin, WHEN haku käsitellään, THEN turvallinen virheluokka tallentuu tai palautuu detail-specin mukaan.
- [ ] #2 GIVEN adapteri palauttaa rate limit -tilanteen, WHEN haku käsitellään, THEN kutsurajaa kunnioitetaan eikä hallitsematonta retry-silmukkaa synny.
- [ ] #3 GIVEN adapteri palauttaa raw-lähdevirheen, WHEN vastaus tai lokit muodostetaan, THEN raw-virhettä, API-avainta tai credentialia ei paljasteta.
- [ ] #4 GIVEN epäonnistunut haku käsitellään, WHEN aiempaa markkinadataa on tallennettuna, THEN aiempi data ei korruptoidu.
- [ ] #5 GIVEN tuotantorajaa arvioidaan, WHEN oikea EODHD-kutsu tarvittaisiin, THEN tehtävä merkitään Blocked siltä osin ilman tuotantokutsua.
<!-- AC:END -->

## Definition of Done
<!-- DOD:BEGIN -->
- [ ] #1 Acceptance criteria on testattu tehtävän scopea vasten
- [ ] #2 Relevantit lint typecheck build ja testikomennot on ajettu tai rajaus on kirjattu
- [ ] #3 Salaisuuksia tokeneita credentialeja ja PII-tietoja ei palauteta lokiteta tai commitoida
- [ ] #4 Julkiset API data infra ja operointisopimukset on päivitetty tarvittaessa
- [ ] #5 Final Summary kuvaa toteutuksen tuloksen validoinnin ja rajaukset
<!-- DOD:END -->
