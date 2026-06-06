---
id: TASK-008
title: Toteuta DisableUser-usecase
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
ordinal: 7000
---

## Description

<!-- SECTION:DESCRIPTION:BEGIN -->
### MITÄ
Toteuta Auth-kontekstin käyttäjätilin deaktivointi.

- Tarjoa REST-rajapinnat `PATCH /auth/users/disable` ja `PUT /auth/users/disable`.
- Vaadi auktorisoinniksi rooli vähintään `ADMIN`.
- Hyväksy query-parametrina `email`.
- Lataa käyttäjä sähköpostilla `IUserRepository`-portin kautta.
- Kutsu `User.disable`-toimintoa ja persistoi päivitys.
- Palauta onnistuneesta deaktivoinnista no content -vastaus.

### MIKSI
Admin-käyttäjän pitää pystyä estämään käyttäjätilin käyttö ilman tilin poistamista. Usecase varmistaa, että deaktivointi tapahtuu domain-mallin kautta ja että vain admin-rooli voi muuttaa käyttäjän enabled-tilaa.
<!-- SECTION:DESCRIPTION:END -->

## Acceptance Criteria
<!-- AC:BEGIN -->
- [ ] #1 GIVEN enabled user, WHEN `PATCH /auth/users/disable` tai `PUT /auth/users/disable` kutsutaan ADMIN-roolilla, THEN vastaus on `204` ja käyttäjä persistetään `enabled=false`.
- [ ] #2 GIVEN missing user, WHEN disable-usecase kutsutaan emaililla, THEN vastaus on `404 Not Found`.
- [ ] #3 GIVEN kutsujan rooli on alle ADMIN, WHEN disable-usecasea kutsutaan, THEN pyyntö hylätään auktorisointivirheenä eikä käyttäjää päivitetä.
- [ ] #4 GIVEN deaktivointi onnistuu, WHEN vastaus muodostetaan, THEN domain-tapahtumia ei julkaista.
<!-- AC:END -->

## Definition of Done
<!-- DOD:BEGIN -->
- [ ] #1 Käyttäjän määrittelemät Spec by Example -esimerkit on huomioitu toteutuksessa.
- [ ] #2 Toteutus on testattu tehtävän acceptance criteria -kohtia vasten.
- [ ] #3 Toteutuksen lopputulos ja mahdolliset rajaukset on kirjattu Final Summary -osioon.
<!-- DOD:END -->
