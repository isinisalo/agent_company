---
id: TASK-004
title: Toteuta RegisterUser-usecase
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
ordinal: 3000
---

## Description

<!-- SECTION:DESCRIPTION:BEGIN -->
### MITÄ
Toteuta Auth-kontekstin käyttäjän rekisteröinti.

- Tarjoa REST-rajapinta `POST /auth/register` roolille vähintään `GUEST`.
- Hyväksy pyynnössä `name`, `email`, `password`, `role` ja `enabled`.
- Tarkista rekisteröinnin feature flag polusta `/feature/auth/register_user`.
- Varmista, että email on uniikki ennen uuden käyttäjän luontia.
- Luo käyttäjä `User.create`-toiminnolla ja persistoi se `IUserRepository.create_user`-portilla.
- Julkaise `NewUserRegistered`-domain-tapahtuma `EventBus`-portilla.

### MIKSI
Rekisteröinti käynnistää käyttäjän elinkaaren Auth-kontekstissa. Usecase varmistaa, että uudet käyttäjät syntyvät validilla datalla, uniikilla sähköpostilla ja tapahtumalla, jota muu järjestelmä voi hyödyntää esimerkiksi sähköpostivahvistukseen.
<!-- SECTION:DESCRIPTION:END -->

## Acceptance Criteria
<!-- AC:BEGIN -->
- [ ] #1 GIVEN new email, WHEN `POST /auth/register` kutsutaan validilla pyynnöllä, THEN vastaus on `201`, käyttäjä persistetään disabled-tilassa ja `NewUserRegistered` julkaistaan.
- [ ] #2 GIVEN existing email, WHEN `POST /auth/register` kutsutaan samalla emaililla, THEN rekisteröinti hylätään validointivirheenä eikä uutta käyttäjää luoda.
- [ ] #3 GIVEN feature disabled, WHEN `POST /auth/register` kutsutaan, THEN rekisteröinti hylätään eikä käyttäjää persistetä.
- [ ] #4 GIVEN rekisteröinti onnistuu, WHEN `NewUserRegistered` julkaistaan, THEN tapahtuma sisältää version, causation, correlation_id, occurred_at, name, email, role, enabled ja verification_token -kentät.
- [ ] #5 GIVEN pyynnön password ei täytä Password-sääntöjä, WHEN rekisteröintiä yritetään, THEN pyyntö hylätään validointivirheenä.
<!-- AC:END -->

## Definition of Done
<!-- DOD:BEGIN -->
- [ ] #1 Käyttäjän määrittelemät Spec by Example -esimerkit on huomioitu toteutuksessa.
- [ ] #2 Toteutus on testattu tehtävän acceptance criteria -kohtia vasten.
- [ ] #3 Toteutuksen lopputulos ja mahdolliset rajaukset on kirjattu Final Summary -osioon.
<!-- DOD:END -->
