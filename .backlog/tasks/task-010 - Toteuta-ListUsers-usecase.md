---
id: TASK-010
title: Toteuta ListUsers-usecase
status: To Do
assignee: []
created_date: '2026-06-06 08:20'
updated_date: '2026-06-06 08:39'
labels:
  - Backend
  - Auth
milestone: m-1
dependencies:
  - TASK-002
priority: medium
ordinal: 9000
---

## Description

<!-- SECTION:DESCRIPTION:BEGIN -->
### MITÄ
Toteuta Auth-kontekstin käyttäjäsummaryjen listaus.

- Tarjoa REST-rajapinta `GET /auth/users`.
- Vaadi auktorisoinniksi rooli vähintään `READER`.
- Lataa käyttäjäkokoelma `IUserRepository.list_users`-portin kautta.
- Palauta käyttäjäsummary-lista.
- Palauta tyhjä lista, kun käyttäjiä ei ole.

### MIKSI
Käyttäjien hallinta ja tarkastelu edellyttää listausrajapintaa, jota vähintään reader-tason käyttäjät voivat käyttää. Usecase määrittää kevyen lukupolun ilman käyttäjän muokkausta tai domain-tapahtumia.
<!-- SECTION:DESCRIPTION:END -->

## Acceptance Criteria
<!-- AC:BEGIN -->
- [ ] #1 GIVEN users exist, WHEN `GET /auth/users` kutsutaan roolilla vähintään READER, THEN vastaus on `200` ja sisältää user summary list -vastauksen.
- [ ] #2 GIVEN no users, WHEN `GET /auth/users` kutsutaan roolilla vähintään READER, THEN vastaus on `200` ja sisältää tyhjän listan.
- [ ] #3 GIVEN kutsujan rooli on alle READER, WHEN list-users-usecasea kutsutaan, THEN pyyntö hylätään auktorisointivirheenä.
- [ ] #4 GIVEN listaus suoritetaan, WHEN käyttäjät haetaan, THEN käytetään `IUserRepository.list_users`-porttia eikä käyttäjiä persistetä.
- [ ] #5 GIVEN listaus onnistuu, WHEN vastaus muodostetaan, THEN domain-tapahtumia ei julkaista.
<!-- AC:END -->

## Definition of Done
<!-- DOD:BEGIN -->
- [ ] #1 Käyttäjän määrittelemät Spec by Example -esimerkit on huomioitu toteutuksessa.
- [ ] #2 Toteutus on testattu tehtävän acceptance criteria -kohtia vasten.
- [ ] #3 Toteutuksen lopputulos ja mahdolliset rajaukset on kirjattu Final Summary -osioon.
<!-- DOD:END -->
