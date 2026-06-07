---
id: TASK-030
title: 'Marketdata: Hae markkinadata mock-only EODHD-adapterilla'
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
  - TASK-029
references:
  - >-
    .backlog/tasks/task-018 -
    Detail-spec-Marketdata-collection-and-query-contract.md
documentation:
  - .backlog/docs/intent/goal.md
  - .backlog/docs/specs/doc-006 - bounded-context-map-and-glossary.md
  - .backlog/docs/specs/doc-010 - external-data-source-compliance.md
priority: medium
ordinal: 1000
---

## Description

<!-- SECTION:DESCRIPTION:BEGIN -->
### MITÄ
Toteuta Marketdata-kontekstin käyttötapaus, jossa seurattavalle yritykselle haetaan markkinadataa mock-only EODHD-adapterilla.

- Haku kohdistuu Companies/watchlist-kontekstissa seurattavaan yritykseen.
- Adapteri ei tee tuotantokutsua EODHD:hen.
- Raw EODHD -malli normalisoidaan Marketdata-kontekstin kielelle.

### MIKSI
Markkinadatan keruupolku tarvitaan ennen tuotantointegraatiota, mutta EODHD-tuotantokäyttö vaatii erillisen compliance-evidenssin.
<!-- SECTION:DESCRIPTION:END -->

## Acceptance Criteria
<!-- AC:BEGIN -->
- [ ] #1 GIVEN seurattava yritys ja validi mock-only EODHD-vastaus, WHEN markkinadata haetaan, THEN normalisoitu markkinadata syntyy tallennusta varten.
- [ ] #2 GIVEN yritys ei ole seurannassa, WHEN hakua yritetään, THEN haku hylätään eikä markkinadataa synny.
- [ ] #3 GIVEN mock-vastaus on virheellinen, WHEN haku käsitellään, THEN virhe palautuu turvallisena virheluokkana ilman raw-lähdevirhettä.
- [ ] #4 GIVEN EODHD-tuotantokutsu tai oikea API-avain tarvittaisiin, WHEN toteutusta arvioidaan, THEN tehtävä merkitään Blocked siltä osin eikä tuotantokutsua toteuteta.
- [ ] #5 GIVEN vastaus tai lokit muodostetaan, WHEN haku onnistuu tai epäonnistuu, THEN API-avaimia, credentialeja tai raw EODHD -mallia ei palauteta eikä lokiteta.
<!-- AC:END -->

## Definition of Done
<!-- DOD:BEGIN -->
- [ ] #1 Acceptance criteria on testattu tehtävän scopea vasten
- [ ] #2 Relevantit lint typecheck build ja testikomennot on ajettu tai rajaus on kirjattu
- [ ] #3 Salaisuuksia tokeneita credentialeja ja PII-tietoja ei palauteta lokiteta tai commitoida
- [ ] #4 Julkiset API data infra ja operointisopimukset on päivitetty tarvittaessa
- [ ] #5 Final Summary kuvaa toteutuksen tuloksen validoinnin ja rajaukset
<!-- DOD:END -->
