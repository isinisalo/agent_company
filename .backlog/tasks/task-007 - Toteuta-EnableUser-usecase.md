---
id: TASK-007
title: Toteuta EnableUser-usecase
status: To Do
assignee: []
created_date: '2026-06-06 08:19'
updated_date: '2026-06-06 08:39'
labels:
  - Backend
  - Auth
milestone: m-1
dependencies:
  - TASK-002
priority: medium
ordinal: 6000
---

## Description

<!-- SECTION:DESCRIPTION:BEGIN -->
### MITÄ
Toteuta Auth-kontekstin käyttäjätilin aktivointi.

- Tarjoa REST-rajapinnat `PATCH /auth/enable` ja `PUT /auth/enable`.
- Vaadi auktorisoinniksi rooli vähintään `ADMIN`.
- Hyväksy query-parametrina `email`.
- Lataa käyttäjä sähköpostilla `IUserRepository`-portin kautta.
- Kutsu `User.enable`-toimintoa ja persistoi päivitys.
- Palauta aktivoinnin tila vastauksessa.

### MIKSI
Admin-käyttäjän pitää pystyä palauttamaan tai aktivoimaan käyttäjätili hallitusti. Usecase keskittää aktivoinnin domain-sääntöihin ja varmistaa, että vain admin-rooli voi muuttaa käyttäjän enabled-tilaa.
<!-- SECTION:DESCRIPTION:END -->

## Acceptance Criteria
<!-- AC:BEGIN -->
- [ ] #1 GIVEN disabled user, WHEN `PATCH /auth/enable` tai `PUT /auth/enable` kutsutaan ADMIN-roolilla, THEN vastaus on `200`, enabled response palautetaan ja käyttäjä persistetään `enabled=true`.
- [ ] #2 GIVEN missing user, WHEN enable-usecase kutsutaan emaililla, THEN vastaus on `404 Not Found`.
- [ ] #3 GIVEN kutsujan rooli on alle ADMIN, WHEN enable-usecasea kutsutaan, THEN pyyntö hylätään auktorisointivirheenä eikä käyttäjää päivitetä.
- [ ] #4 GIVEN aktivointi onnistuu, WHEN vastaus muodostetaan, THEN domain-tapahtumia ei julkaista.
<!-- AC:END -->

## Definition of Done
<!-- DOD:BEGIN -->
- [ ] #1 Käyttäjän määrittelemät Spec by Example -esimerkit on huomioitu toteutuksessa.
- [ ] #2 Toteutus on testattu tehtävän acceptance criteria -kohtia vasten.
- [ ] #3 Toteutuksen lopputulos ja mahdolliset rajaukset on kirjattu Final Summary -osioon.
<!-- DOD:END -->
