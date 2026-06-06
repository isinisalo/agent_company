---
id: TASK-005
title: Toteuta VerifyEmail-usecase
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
ordinal: 4000
---

## Description

<!-- SECTION:DESCRIPTION:BEGIN -->
### MITÄ
Toteuta Auth-kontekstin sähköpostivahvistus.

- Tarjoa julkinen REST-rajapinta `GET /auth/verify-email`.
- Hyväksy query-parametreina `email` ja `token`.
- Lataa käyttäjä sähköpostilla `IUserRepository`-portista.
- Varmista token `User.verify_email`-toiminnolla.
- Persistoi käyttäjän päivitys `IUserRepository.update`-portilla.
- Palauta vahvistuksen tila vastauksessa.

### MIKSI
Sähköpostivahvistus viimeistelee rekisteröinnin ja aktivoi käyttäjän käyttöön. Usecase varmistaa, että vain oikealla vahvistustokenilla käyttäjän email hyväksytään ja verification_token poistetaan käytöstä.
<!-- SECTION:DESCRIPTION:END -->

## Acceptance Criteria
<!-- AC:BEGIN -->
- [ ] #1 GIVEN matching token, WHEN `GET /auth/verify-email` kutsutaan emaililla ja tokenilla, THEN vastaus on `200`, käyttäjä on `enabled=true` ja `verification_token` on tyhjennetty.
- [ ] #2 GIVEN invalid token, WHEN `GET /auth/verify-email` kutsutaan, THEN vahvistus hylätään validointivirheenä eikä käyttäjää aktivoida.
- [ ] #3 GIVEN käyttäjä löytyy ja token täsmää, WHEN vahvistus onnistuu, THEN käyttäjä päivitetään `IUserRepository.update`-portin kautta.
- [ ] #4 GIVEN sähköpostivahvistus onnistuu tai epäonnistuu, WHEN vastaus muodostetaan, THEN domain-tapahtumia ei julkaista.
<!-- AC:END -->

## Definition of Done
<!-- DOD:BEGIN -->
- [ ] #1 Käyttäjän määrittelemät Spec by Example -esimerkit on huomioitu toteutuksessa.
- [ ] #2 Toteutus on testattu tehtävän acceptance criteria -kohtia vasten.
- [ ] #3 Toteutuksen lopputulos ja mahdolliset rajaukset on kirjattu Final Summary -osioon.
<!-- DOD:END -->
