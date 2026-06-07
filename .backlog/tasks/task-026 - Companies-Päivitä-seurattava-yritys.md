---
id: TASK-026
title: 'Companies: Päivitä seurattava yritys'
status: To Do
assignee: []
created_date: '2026-06-07 11:25'
labels:
  - Companies
  - Backend
milestone: m-5
dependencies:
  - TASK-017
references:
  - .backlog/tasks/task-017 - Detail-spec-Companies-and-watchlist-contract.md
documentation:
  - .backlog/docs/intent/goal.md
  - .backlog/docs/specs/doc-006 - bounded-context-map-and-glossary.md
priority: medium
ordinal: 2000
---

## Description

<!-- SECTION:DESCRIPTION:BEGIN -->
### MITÄ
Toteuta Companies and watchlist -kontekstin käyttötapaus, jossa ylläpitäjä muokkaa seurattavan yrityksen hallittavia tietoja ja keruuasetuksia.

- Päivitys kohdistuu olemassa olevaan seurattavaan yritykseen.
- Vain detail-specissä muokattavaksi määritetyt kentät muuttuvat.
- Päivitys ei muuta Marketdata- tai Comments-kontekstien kerättyä dataa suoraan.

### MIKSI
Ylläpitäjän pitää pystyä korjaamaan yrityksen tietoja ja keruuasetuksia ilman muiden contextien omistaman datan sivuvaikutuksia.
<!-- SECTION:DESCRIPTION:END -->

## Acceptance Criteria
<!-- AC:BEGIN -->
- [ ] #1 GIVEN seurattava yritys on olemassa ja syöte on validi, WHEN yritystä päivitetään, THEN sallitut tiedot muuttuvat.
- [ ] #2 GIVEN päivitys yrittää muuttaa kiellettyä kenttää, WHEN pyyntö käsitellään, THEN muutos hylätään eikä yritys muutu.
- [ ] #3 GIVEN yritystä ei löydy, WHEN päivitystä yritetään, THEN pyyntö hylätään eikä uutta yritystä luoda.
- [ ] #4 GIVEN kutsuja ei ole hallintakäyttäjä, WHEN päivitystä yritetään, THEN toiminto hylätään ennen muutosta.
- [ ] #5 GIVEN päivitys onnistuu, WHEN muutoksen vaikutus arvioidaan, THEN Marketdata- tai Comments-dataa ei muuteta tässä käyttötapauksessa.
<!-- AC:END -->

## Definition of Done
<!-- DOD:BEGIN -->
- [ ] #1 Acceptance criteria on testattu tehtävän scopea vasten
- [ ] #2 Relevantit lint typecheck build ja testikomennot on ajettu tai rajaus on kirjattu
- [ ] #3 Salaisuuksia tokeneita credentialeja ja PII-tietoja ei palauteta lokiteta tai commitoida
- [ ] #4 Julkiset API data infra ja operointisopimukset on päivitetty tarvittaessa
- [ ] #5 Final Summary kuvaa toteutuksen tuloksen validoinnin ja rajaukset
<!-- DOD:END -->
