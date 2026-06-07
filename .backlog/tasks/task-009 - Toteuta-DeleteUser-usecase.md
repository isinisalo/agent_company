---
id: TASK-009
title: 'Auth: Käyttäjän poisto'
status: To Do
assignee: []
created_date: '2026-06-06 08:20'
updated_date: '2026-06-07 12:19'
labels:
  - Backend
  - Auth
milestone: m-1
dependencies:
  - TASK-015
references:
  - >-
    .backlog/tasks/task-015 -
    Detail-spec-Auth-domain-API-ja-persistence-contract.md
documentation:
  - .backlog/docs/intent/doc-001 - goal.md
  - .backlog/docs/specs/doc-006 - bounded-context-map-and-glossary.md
priority: medium
ordinal: 8000
---

## Description

<!-- SECTION:DESCRIPTION:BEGIN -->
### MITÄ
Toteuta Auth-kontekstin admin-toiminto käyttäjän poistamiseen Auth detail-specin ja tämän tehtävän acceptance criteria -kohtien mukaisesti.

- Vain hallintakäyttäjä voi poistaa Auth-käyttäjän.
- Poisto kohdistuu käyttäjään Auth detail-specissä määritetyllä tunnisteella.
- Poisto on idempotentti myös silloin, kun käyttäjää ei löydy.
- Poiston scope rajataan Auth bounded contextin käyttäjä-, credential- ja vahvistustietoihin.
- Salaisuuksia ei palauteta, julkaista tai lokiteta.

### MIKSI
Adminin pitää pystyä poistamaan Auth-käyttäjätili järjestelmästä. Idempotentti poisto tekee toiminnosta vakaan myös uudelleenyrityksissä, mutta audit-, privacy- ja laajemmat datanpoistopolitiikat vaativat erillisen päätöksen ennen tuotantolaajennusta.
<!-- SECTION:DESCRIPTION:END -->

## Acceptance Criteria
<!-- AC:BEGIN -->
- [ ] #1 GIVEN käyttäjä on olemassa ja kutsuja on hallintakäyttäjä, WHEN käyttäjä poistetaan, THEN Auth-käyttäjä poistetaan.
- [ ] #2 GIVEN käyttäjää ei löydy ja kutsuja on hallintakäyttäjä, WHEN käyttäjää poistetaan, THEN toiminto onnistuu idempotentisti eikä uutta käyttäjää luoda.
- [ ] #3 GIVEN kutsuja ei ole hallintakäyttäjä, WHEN käyttäjän poistoa yritetään, THEN toiminto hylätään eikä poistoa tehdä.
- [ ] #4 GIVEN poiston scopea arvioidaan, WHEN tehtävä toteutetaan, THEN se koskee vain Auth bounded contextin käyttäjä-, credential- ja vahvistustietoja eikä määritä audit-retentiota, anonymisointia tai muiden bounded contextien datapoistoa.
- [ ] #5 GIVEN poisto onnistuu tai käyttäjää ei löydy, WHEN vastaus ja lokit muodostetaan, THEN credential- tai vahvistussalaisuuksia ei palauteta, julkaista tai lokiteta.
<!-- AC:END -->

## Definition of Done
<!-- DOD:BEGIN -->
- [ ] #1 Käyttäjän määrittelemät Spec by Example -esimerkit on huomioitu toteutuksessa.
- [ ] #2 Toteutus on testattu tehtävän acceptance criteria -kohtia vasten.
- [ ] #3 Toteutuksen lopputulos ja mahdolliset rajaukset on kirjattu Final Summary -osioon.
<!-- DOD:END -->
