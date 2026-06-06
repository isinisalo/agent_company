---
id: TASK-003
title: Toteuta AuthenticateCommand-usecase
status: To Do
assignee: []
created_date: '2026-06-06 08:18'
updated_date: '2026-06-06 08:39'
labels:
  - Backend
  - Auth
milestone: m-1
dependencies:
  - TASK-002
priority: medium
ordinal: 2000
---

## Description

<!-- SECTION:DESCRIPTION:BEGIN -->
### MITÄ
Toteuta Auth-kontekstin käyttäjän autentikointi.

- Tarjoa julkinen REST-rajapinta `POST /auth/token`.
- Hyväksy pyynnössä `email` ja `password`.
- Lataa käyttäjä sähköpostilla `IUserRepository`-portin kautta.
- Varmista salasana `User.ensure_password`-toiminnolla.
- Palauta onnistuneesta kirjautumisesta RS256-allekirjoitettu JWT-token.
- Päivitä käyttäjä vain, jos legacy-salasanahash rehashataan.

### MIKSI
Käyttäjien kirjautuminen on Auth-kokonaisuuden peruskyvykkyys. Usecase varmistaa, että vain tunnetut ja enabled-tilassa olevat käyttäjät saavat käyttöönsä API-autentikointiin tarvittavan JWT-tokenin.
<!-- SECTION:DESCRIPTION:END -->

## Acceptance Criteria
<!-- AC:BEGIN -->
- [ ] #1 GIVEN valid credentials, WHEN `POST /auth/token` kutsutaan, THEN vastaus on `201` ja sisältää JWT-tokenin.
- [ ] #2 GIVEN unknown email, WHEN `POST /auth/token` kutsutaan, THEN vastaus on `401 Unauthorized`.
- [ ] #3 GIVEN disabled user, WHEN `POST /auth/token` kutsutaan oikealla salasanalla, THEN vastaus on `401 Unauthorized`.
- [ ] #4 GIVEN legacy password hash tarvitsee rehashauksen, WHEN autentikointi onnistuu, THEN päivitetty käyttäjä persistetään `IUserRepository.update`-portin kautta.
- [ ] #5 GIVEN autentikointi epäonnistuu, WHEN vastaus muodostetaan, THEN domain-tapahtumia ei julkaista.
<!-- AC:END -->

## Definition of Done
<!-- DOD:BEGIN -->
- [ ] #1 Käyttäjän määrittelemät Spec by Example -esimerkit on huomioitu toteutuksessa.
- [ ] #2 Toteutus on testattu tehtävän acceptance criteria -kohtia vasten.
- [ ] #3 Toteutuksen lopputulos ja mahdolliset rajaukset on kirjattu Final Summary -osioon.
<!-- DOD:END -->
