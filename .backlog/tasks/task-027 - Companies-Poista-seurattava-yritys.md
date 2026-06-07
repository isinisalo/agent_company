---
id: TASK-027
title: 'Companies: Poista seurattava yritys'
status: To Do
assignee: []
created_date: '2026-06-07 11:26'
labels:
  - Companies
  - Backend
milestone: m-5
dependencies:
  - TASK-017
references:
  - .backlog/tasks/task-017 - Detail-spec-Companies-and-watchlist-contract.md
documentation:
  - .backlog/docs/intent/doc-001 - goal.md
  - .backlog/docs/specs/doc-006 - bounded-context-map-and-glossary.md
priority: medium
ordinal: 3000
---

## Description

<!-- SECTION:DESCRIPTION:BEGIN -->
### MITÄ
Toteuta Companies and watchlist -kontekstin käyttötapaus, jossa ylläpitäjä poistaa yrityksen seurannasta.

- Poisto kohdistuu Companies/watchlist-kontekstin seuranta- ja asetustietoihin.
- Poisto ei määritä muiden contextien datapoistoa, anonymisointia tai retentionia.
- Toiminto on turvallinen uudelleenyrityksille detail-specin mukaan.

### MIKSI
Ylläpitäjän pitää pystyä lopettamaan yrityksen seuranta ilman, että samalla arvataan muiden contextien datan säilytyspolitiikkaa.
<!-- SECTION:DESCRIPTION:END -->

## Acceptance Criteria
<!-- AC:BEGIN -->
- [ ] #1 GIVEN seurattava yritys on olemassa ja kutsuja on hallintakäyttäjä, WHEN yritys poistetaan seurannasta, THEN se ei enää näy seurattavana yrityksenä.
- [ ] #2 GIVEN yritystä ei löydy, WHEN poistoa yritetään, THEN toiminto on idempotentti tai hylätään detail-specin mukaisesti ilman uuden yrityksen luontia.
- [ ] #3 GIVEN kutsuja ei ole hallintakäyttäjä, WHEN poistoa yritetään, THEN toiminto hylätään ennen muutosta.
- [ ] #4 GIVEN poiston scopea arvioidaan, WHEN tehtävä toteutetaan, THEN se ei poista Marketdata- tai Comments-kontekstien dataa eikä päätä cross-context retentionia.
- [ ] #5 GIVEN poisto onnistuu tai hylätään, WHEN vastaus ja lokit muodostetaan, THEN salaisuuksia, credentialeja tai lähteen raw-dataa ei palauteta eikä lokiteta.
<!-- AC:END -->

## Definition of Done
<!-- DOD:BEGIN -->
- [ ] #1 Acceptance criteria on testattu tehtävän scopea vasten
- [ ] #2 Relevantit lint typecheck build ja testikomennot on ajettu tai rajaus on kirjattu
- [ ] #3 Salaisuuksia tokeneita credentialeja ja PII-tietoja ei palauteta lokiteta tai commitoida
- [ ] #4 Julkiset API data infra ja operointisopimukset on päivitetty tarvittaessa
- [ ] #5 Final Summary kuvaa toteutuksen tuloksen validoinnin ja rajaukset
<!-- DOD:END -->
