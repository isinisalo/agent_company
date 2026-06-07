---
id: TASK-007
title: 'Auth: Käyttäjän käyttöönotto'
status: To Do
assignee: []
created_date: '2026-06-06 08:19'
updated_date: '2026-06-07 11:24'
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
  - .backlog/docs/governance/Agenttien päätöksenteon reunaehdot.md
  - .backlog/docs/specs/doc-006 - bounded-context-map-and-glossary.md
priority: medium
ordinal: 6000
---

## Description

<!-- SECTION:DESCRIPTION:BEGIN -->
### MITÄ
Toteuta Auth-kontekstin admin-toiminto käyttäjän käytön sallimiseen Auth detail-specin ja tämän tehtävän acceptance criteria -kohtien mukaisesti.

- Vain hallintakäyttäjä voi sallia käyttäjän käytön.
- Toiminto kohdistuu käyttäjään Auth detail-specissä määritetyllä tunnisteella.
- Toiminto on idempotentti, jos käyttäjän käyttö on jo sallittu.
- Toiminto ei muuta sähköpostivahvistuksen tilaa.
- Salaisuuksia ei palauteta, julkaista tai lokiteta.

### MIKSI
Adminin pitää pystyä palauttamaan käyttäjätilin käyttöoikeus ilman, että sähköpostivahvistuksen tila muuttuu. Käyttötapaus erottaa adminin käyttöeston sähköpostivahvistuksesta ja rajaa muutoksen vain hallintakäyttäjälle.
<!-- SECTION:DESCRIPTION:END -->

## Acceptance Criteria
<!-- AC:BEGIN -->
- [ ] #1 GIVEN käyttäjän käyttö on estetty ja kutsuja on hallintakäyttäjä, WHEN käyttäjän käyttö sallitaan, THEN toiminto onnistuu ja käyttäjän käyttö muuttuu sallituksi.
- [ ] #2 GIVEN käyttäjän käyttö on jo sallittu ja kutsuja on hallintakäyttäjä, WHEN käyttäjän käyttö sallitaan uudelleen, THEN toiminto onnistuu idempotentisti.
- [ ] #3 GIVEN käyttäjä löytyy, WHEN käyttäjän käyttö sallitaan, THEN sähköpostivahvistuksen tila ei muutu.
- [ ] #4 GIVEN käyttäjää ei löydy ja kutsuja on hallintakäyttäjä, WHEN käyttäjän käyttöä yritetään sallia, THEN toiminto hylätään puuttuvan käyttäjänä eikä uutta käyttäjää luoda.
- [ ] #5 GIVEN kutsuja ei ole hallintakäyttäjä, WHEN käyttäjän käyttöä yritetään sallia, THEN toiminto hylätään ennen käyttäjän muuttamista.
- [ ] #6 GIVEN käyttöönotto onnistuu tai epäonnistuu, WHEN vastaus ja lokit muodostetaan, THEN credential- tai vahvistussalaisuuksia ei palauteta, julkaista tai lokiteta.
<!-- AC:END -->

## Definition of Done
<!-- DOD:BEGIN -->
- [ ] #1 Käyttäjän määrittelemät Spec by Example -esimerkit on huomioitu toteutuksessa.
- [ ] #2 Toteutus on testattu tehtävän acceptance criteria -kohtia vasten.
- [ ] #3 Toteutuksen lopputulos ja mahdolliset rajaukset on kirjattu Final Summary -osioon.
<!-- DOD:END -->
