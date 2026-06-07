---
id: TASK-017
title: 'Detail spec: Companies and watchlist contract'
status: To Do
assignee: []
created_date: '2026-06-07 11:22'
updated_date: '2026-06-07 12:19'
labels:
  - Companies
  - Spec
  - Backend
milestone: m-3
dependencies:
  - TASK-013
documentation:
  - .backlog/docs/intent/doc-001 - goal.md
  - .backlog/docs/specs/doc-006 - bounded-context-map-and-glossary.md
  - .backlog/docs/specs/doc-010 - external-data-source-compliance.md
priority: medium
ordinal: 2200
---

## Description

<!-- SECTION:DESCRIPTION:BEGIN -->
### MITÄ
Määritä Companies and watchlist bounded contextin HOW-tason domain-, API-, persistence-, YTJ-adapteri- ja testisopimus hyväksyttyjen projektirajojen sisällä.

Specin pitää tukea seurattavan yrityksen lisäämistä, muokkausta, poistoa, listausta ja perustietojen mock-only-päivitystä.

### MIKSI
Yritykset ja seurantalista määrittävät, mitä dataa muut keruukontekstit hakevat.
<!-- SECTION:DESCRIPTION:END -->

## Acceptance Criteria
<!-- AC:BEGIN -->
- [ ] #1 GIVEN Companies detail-spec tehdään, WHEN tehtävä valmistuu, THEN spec kuvaa tracked companyn ja watchlistin vastuut käyttötapausten kannalta riittävästi.
- [ ] #2 GIVEN YTJ-adapteria suunnitellaan, WHEN spec luetaan, THEN raw YTJ -malli ei vuoda domainiin tai julkiseen API:in.
- [ ] #3 GIVEN yrityksen keruuasetukset vaikuttavat Marketdataan tai Commentsiin, WHEN spec luetaan, THEN handoff on kuvattu ilman toisen contextin domain-sääntöjen omimista.
- [ ] #4 GIVEN YTJ-tuotantokäyttöä arvioidaan, WHEN agentti tarkistaa specin, THEN mock-only/compliance-raja on eksplisiittinen.
<!-- AC:END -->

## Definition of Done
<!-- DOD:BEGIN -->
- [ ] #1 Acceptance criteria on testattu tehtävän scopea vasten
- [ ] #2 Relevantit lint typecheck build ja testikomennot on ajettu tai rajaus on kirjattu
- [ ] #3 Salaisuuksia tokeneita credentialeja ja PII-tietoja ei palauteta lokiteta tai commitoida
- [ ] #4 Julkiset API data infra ja operointisopimukset on päivitetty tarvittaessa
- [ ] #5 Final Summary kuvaa toteutuksen tuloksen validoinnin ja rajaukset
<!-- DOD:END -->
