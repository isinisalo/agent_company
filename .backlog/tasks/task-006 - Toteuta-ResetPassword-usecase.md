---
id: TASK-006
title: Toteuta ResetPassword-usecase
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
ordinal: 5000
---

## Description

<!-- SECTION:DESCRIPTION:BEGIN -->
### MITÄ
Toteuta Auth-kontekstin salasanan resetointipyynnön käynnistys.

- Tarjoa julkinen REST-rajapinta `POST /auth/reset-password`.
- Hyväksy pyynnössä `email`.
- Lataa olemassa oleva käyttäjä sähköpostilla `IUserRepository`-portin kautta.
- Kutsu `User.request_password_reset`-toimintoa.
- Julkaise `ResetPasswordRequested`-domain-tapahtuma `EventBus`-portilla.
- Palauta pyynnön vastaanotettu tila vastauksessa.

### MIKSI
Salasanan resetointi mahdollistaa tilin palauttamisen ilman kirjautunutta sessiota. Usecase rajaa vastuun reset-tokenin pyytämiseen ja tapahtuman julkaisuun, jotta varsinainen viestin lähetys voidaan hoitaa tapahtumankäsittelyssä.
<!-- SECTION:DESCRIPTION:END -->

## Acceptance Criteria
<!-- AC:BEGIN -->
- [ ] #1 GIVEN existing user, WHEN `POST /auth/reset-password` kutsutaan käyttäjän emaililla, THEN vastaus on `202`, requested response palautetaan ja `ResetPasswordRequested` julkaistaan.
- [ ] #2 GIVEN missing user, WHEN `POST /auth/reset-password` kutsutaan tuntemattomalla emaililla, THEN vastaus on `404 Not Found`.
- [ ] #3 GIVEN resetointipyyntö onnistuu, WHEN `ResetPasswordRequested` julkaistaan, THEN tapahtuma sisältää version, causation, correlation_id, occurred_at, name, email ja reset_token -kentät.
- [ ] #4 GIVEN resetointipyyntö käsitellään, WHEN usecase päättyy, THEN käyttäjää ei persistetä tämän usecasen aikana.
<!-- AC:END -->

## Definition of Done
<!-- DOD:BEGIN -->
- [ ] #1 Käyttäjän määrittelemät Spec by Example -esimerkit on huomioitu toteutuksessa.
- [ ] #2 Toteutus on testattu tehtävän acceptance criteria -kohtia vasten.
- [ ] #3 Toteutuksen lopputulos ja mahdolliset rajaukset on kirjattu Final Summary -osioon.
<!-- DOD:END -->
