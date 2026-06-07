---
id: TASK-008
title: 'Auth: Käyttäjän käytöstä poisto'
status: To Do
assignee: []
created_date: '2026-06-06 08:19'
updated_date: '2026-06-07 10:36'
labels:
  - Backend
  - Auth
milestone: m-1
dependencies:
  - TASK-012
  - TASK-013
  - TASK-014
references:
  - .backlog/decisions/*.md
  - .backlog/docs/intent/goal.md
  - .backlog/docs/governance/Agenttien päätöksenteon reunaehdot.md
priority: medium
ordinal: 7000
---

## Description

<!-- SECTION:DESCRIPTION:BEGIN -->
### MITÄ
Toteuta Auth-kontekstin admin-toiminto käyttäjän käytön estämiseen hyväksyttyjen Auth-päätösten mukaisesti.

- Vain hallintakäyttäjä voi estää käyttäjän käytön.
- Toiminto kohdistuu käyttäjään hyväksytyn rajapintasopimuksen mukaisella tunnisteella.
- Toiminto on idempotentti, jos käyttäjän käyttö on jo estetty.
- Toiminto ei muuta sähköpostivahvistuksen tilaa.
- Salaisuuksia ei palauteta, julkaista tai lokiteta.

### MIKSI
Adminin pitää pystyä estämään käyttäjätilin API-käyttö ilman tilin poistamista ja ilman, että sähköpostivahvistuksen tila muuttuu. Käyttötapaus keskittää käyttöeston Auth-domainiin ja rajaa muutoksen vain hallintakäyttäjälle.
<!-- SECTION:DESCRIPTION:END -->

## Acceptance Criteria
<!-- AC:BEGIN -->
- [ ] #1 GIVEN käyttäjän käyttö on sallittu ja kutsuja on hallintakäyttäjä, WHEN käyttäjän käyttö estetään, THEN toiminto onnistuu ja käyttäjän käyttö muuttuu estetyksi.
- [ ] #2 GIVEN käyttäjän käyttö on jo estetty ja kutsuja on hallintakäyttäjä, WHEN käyttäjän käyttö estetään uudelleen, THEN toiminto onnistuu idempotentisti.
- [ ] #3 GIVEN käyttäjä löytyy, WHEN käyttäjän käyttö estetään, THEN sähköpostivahvistuksen tila ei muutu.
- [ ] #4 GIVEN käyttäjää ei löydy ja kutsuja on hallintakäyttäjä, WHEN käyttäjän käyttöä yritetään estää, THEN toiminto hylätään puuttuvan käyttäjänä eikä uutta käyttäjää luoda.
- [ ] #5 GIVEN kutsuja ei ole hallintakäyttäjä, WHEN käyttäjän käyttöä yritetään estää, THEN toiminto hylätään ennen käyttäjän muuttamista.
- [ ] #6 GIVEN käytöstä poisto onnistuu tai epäonnistuu, WHEN vastaus ja lokit muodostetaan, THEN credential- tai vahvistussalaisuuksia ei palauteta, julkaista tai lokiteta.
<!-- AC:END -->

## Definition of Done
<!-- DOD:BEGIN -->
- [ ] #1 Käyttäjän määrittelemät Spec by Example -esimerkit on huomioitu toteutuksessa.
- [ ] #2 Toteutus on testattu tehtävän acceptance criteria -kohtia vasten.
- [ ] #3 Toteutuksen lopputulos ja mahdolliset rajaukset on kirjattu Final Summary -osioon.
<!-- DOD:END -->
