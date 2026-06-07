---
id: TASK-028
title: 'Companies: Listaa seurattavat yritykset'
status: To Do
assignee: []
created_date: '2026-06-07 11:26'
labels:
  - Companies
  - Backend
  - Frontend
milestone: m-5
dependencies:
  - TASK-017
references:
  - .backlog/tasks/task-017 - Detail-spec-Companies-and-watchlist-contract.md
documentation:
  - .backlog/docs/intent/goal.md
  - .backlog/docs/specs/doc-006 - bounded-context-map-and-glossary.md
priority: medium
ordinal: 4000
---

## Description

<!-- SECTION:DESCRIPTION:BEGIN -->
### MITÄ
Toteuta Companies and watchlist -kontekstin käyttötapaus, jossa käyttäjä voi tarkastella seurattavien yritysten listaa roolinsa sallimassa laajuudessa.

- Listaus palauttaa rajatun yrityssummaryn.
- Listaus tukee detail-specissä määritettyä sivutusta tai rajausta.
- Summary ei sisällä ulkoisen lähteen raw-mallia.

### MIKSI
Frontend tarvitsee yrityslistan, josta käyttäjä siirtyy yrityskohtaiseen seurantatietoon.
<!-- SECTION:DESCRIPTION:END -->

## Acceptance Criteria
<!-- AC:BEGIN -->
- [ ] #1 GIVEN seurattavia yrityksiä on olemassa ja kutsuja on sallittu, WHEN yrityksiä listataan, THEN palautuu yrityssummaryjen lista.
- [ ] #2 GIVEN seurattavia yrityksiä ei ole, WHEN yrityksiä listataan, THEN palautuu tyhjä lista.
- [ ] #3 GIVEN kutsujalla ei ole oikeutta listaukseen, WHEN listaa pyydetään, THEN toiminto hylätään ennen datan palautusta.
- [ ] #4 GIVEN summary muodostetaan, WHEN tulos palautetaan, THEN se ei sisällä YTJ:n raw-mallia, credentialeja tai tarpeetonta PII:tä.
- [ ] #5 GIVEN tuloksia on enemmän kuin sivulle mahtuu, WHEN listaus palautetaan, THEN seuraavan sivun tieto palautuu detail-specin mukaisesti.
<!-- AC:END -->

## Definition of Done
<!-- DOD:BEGIN -->
- [ ] #1 Acceptance criteria on testattu tehtävän scopea vasten
- [ ] #2 Relevantit lint typecheck build ja testikomennot on ajettu tai rajaus on kirjattu
- [ ] #3 Salaisuuksia tokeneita credentialeja ja PII-tietoja ei palauteta lokiteta tai commitoida
- [ ] #4 Julkiset API data infra ja operointisopimukset on päivitetty tarvittaessa
- [ ] #5 Final Summary kuvaa toteutuksen tuloksen validoinnin ja rajaukset
<!-- DOD:END -->
