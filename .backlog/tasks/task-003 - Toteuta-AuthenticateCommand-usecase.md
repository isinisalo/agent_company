---
id: TASK-003
title: Toteuta Login-usecase
status: To Do
assignee: []
created_date: '2026-06-06 08:18'
updated_date: '2026-06-07 08:56'
labels:
  - Backend
  - Auth
milestone: m-1
dependencies:
  - TASK-002
documentation:
  - >-
    .backlog/decisions/decision-008-[Backend]-Valitaan-JWT-pohjainen-API-autentikointi.md
  - >-
    .backlog/decisions/decision-009-[Backend]-Määritetään-Auth-bounded-context-ja-usecase-sopimukset.md
  - .backlog/docs/governance/Agenttien päätöksenteon reunaehdot.md
priority: medium
ordinal: 2000
---

## Description

<!-- SECTION:DESCRIPTION:BEGIN -->
### MITÄ
Toteuta Auth-kontekstin käyttäjän kirjautuminen ADR-008:n ja ADR-009:n mukaisesti.

- Tarjoa julkinen REST-rajapinta `POST /auth/token`.
- Hyväksy pyynnössä `email` ja `password`.
- Hae käyttäjä normalisoidulla emaililla `IUserRepository`-portin kautta.
- Tarkista salasana `PasswordHasher`-portilla ja käyttäjän login-kelpoisuus `User`-aggregaatin säännöillä.
- Palauta onnistuneesta kirjautumisesta RS256-allekirjoitettu JWT access token.
- Päivitä `last_login_at` ja mahdollinen vanhentunut password hash vain onnistuneen kirjautumisen yhteydessä.

### MIKSI
Kirjautuminen on selaimen ja API:n perusvirta. Usecase varmistaa, että API-tokenin saa vain tunnettu, sähköpostinsa vahvistanut ja adminin sallima käyttäjä ilman, että epäonnistumisen syy paljastaa käyttäjätilin olemassaoloa tai tilaa.
<!-- SECTION:DESCRIPTION:END -->

## Acceptance Criteria
<!-- AC:BEGIN -->
- [ ] #1 GIVEN enabled ja email-vahvistettu käyttäjä sekä oikea salasana, WHEN `POST /auth/token` kutsutaan validilla pyynnöllä, THEN vastaus on `200 OK` ja sisältää JWT access tokenin.
- [ ] #2 GIVEN unknown email, väärä salasana, disabled user tai vahvistamaton email, WHEN `POST /auth/token` kutsutaan, THEN vastaus on sama generic `401 Unauthorized` ilman tarkkaa syytä.
- [ ] #3 GIVEN kirjautuminen onnistuu, WHEN password hash tarvitsee rehashauksen tai `last_login_at` päivittyy, THEN käyttäjä persistetään `IUserRepository.update`-portin kautta.
- [ ] #4 GIVEN pyyntö ei sisällä validia emailia tai salasanaa, WHEN `POST /auth/token` kutsutaan, THEN pyyntö hylätään validointivirheenä ennen salasanatarkistusta.
- [ ] #5 GIVEN autentikointi epäonnistuu tai onnistuu, WHEN vastaus ja lokit muodostetaan, THEN domain-tapahtumia ei julkaista eikä salasanaa, password hashia, JWT:tä tai salaisia avaimia lokiteta.
<!-- AC:END -->



## Definition of Done
<!-- DOD:BEGIN -->
- [ ] #1 Käyttäjän määrittelemät Spec by Example -esimerkit on huomioitu toteutuksessa.
- [ ] #2 Toteutus on testattu tehtävän acceptance criteria -kohtia vasten.
- [ ] #3 Toteutuksen lopputulos ja mahdolliset rajaukset on kirjattu Final Summary -osioon.
<!-- DOD:END -->
