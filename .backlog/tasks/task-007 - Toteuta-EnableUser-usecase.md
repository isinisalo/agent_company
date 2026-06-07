---
id: TASK-007
title: Toteuta EnableUser-usecase
status: To Do
assignee: []
created_date: '2026-06-06 08:19'
updated_date: '2026-06-07 08:58'
labels:
  - Backend
  - Auth
milestone: m-1
dependencies:
  - TASK-002
documentation:
  - >-
    .backlog/decisions/decision-009-[Backend]-Määritetään-Auth-bounded-context-ja-usecase-sopimukset.md
  - .backlog/docs/governance/Agenttien päätöksenteon reunaehdot.md
priority: medium
ordinal: 6000
---

## Description

<!-- SECTION:DESCRIPTION:BEGIN -->
### MITÄ
Toteuta Auth-kontekstin admin-toiminto käyttäjätilin sallimiseen ADR-009:n mukaisesti.

- Tarjoa REST-rajapinta `PATCH /auth/users/enable`.
- Vaadi auktorisoinniksi `ADMIN`-rooli.
- Hyväksy query-parametrina `email`.
- Lataa käyttäjä normalisoidulla emaililla `IUserRepository`-portin kautta.
- Aseta käyttäjän `enabled=true` ja persistoi päivitys.
- Älä muuta käyttäjän `email_verified_at`-arvoa.

### MIKSI
Adminin pitää pystyä palauttamaan käyttäjätilin käyttöoikeus ilman, että sähköpostivahvistuksen tila muuttuu. Usecase erottaa adminin käyttöeston sähköpostivahvistuksesta ja rajaa muutoksen vain `ADMIN`-roolille.
<!-- SECTION:DESCRIPTION:END -->

## Acceptance Criteria
<!-- AC:BEGIN -->
- [ ] #1 GIVEN disabled user ja kutsuja roolilla `ADMIN`, WHEN `PATCH /auth/users/enable?email=...` kutsutaan, THEN vastaus on `204 No Content` ja käyttäjä persistetään `enabled=true`.
- [ ] #2 GIVEN user on jo `enabled=true` ja kutsuja roolilla `ADMIN`, WHEN enable-usecase kutsutaan, THEN vastaus on `204 No Content` ja operaatio on idempotentti.
- [ ] #3 GIVEN käyttäjä löytyy, WHEN enable-usecase onnistuu, THEN `email_verified_at` ei muutu.
- [ ] #4 GIVEN käyttäjää ei löydy ja kutsuja on `ADMIN`, WHEN enable-usecase kutsutaan emaililla, THEN vastaus on `404 Not Found` eikä uutta käyttäjää luoda.
- [ ] #5 GIVEN kutsujan rooli ei ole `ADMIN`, WHEN enable-usecasea kutsutaan, THEN pyyntö hylätään auktorisointivirheenä ennen käyttäjän päivittämistä.
- [ ] #6 GIVEN aktivointi onnistuu tai epäonnistuu, WHEN vastaus ja lokit muodostetaan, THEN domain-tapahtumia ei julkaista eikä credential- tai token-kenttiä lokiteta.
<!-- AC:END -->



## Definition of Done
<!-- DOD:BEGIN -->
- [ ] #1 Käyttäjän määrittelemät Spec by Example -esimerkit on huomioitu toteutuksessa.
- [ ] #2 Toteutus on testattu tehtävän acceptance criteria -kohtia vasten.
- [ ] #3 Toteutuksen lopputulos ja mahdolliset rajaukset on kirjattu Final Summary -osioon.
<!-- DOD:END -->
