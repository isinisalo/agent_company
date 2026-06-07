---
id: TASK-004
title: Toteuta RegisterUser-usecase
status: To Do
assignee: []
created_date: '2026-06-06 08:19'
updated_date: '2026-06-07 09:38'
labels:
  - Backend
  - Auth
milestone: m-1
dependencies:
  - TASK-002
references:
  - >-
    .backlog/decisions/decision-009-[Backend]-Määritetään-Auth-bounded-context-ja-usecase-sopimukset.md
documentation:
  - >-
    .backlog/decisions/decision-009-[Backend]-Määritetään-Auth-bounded-context-ja-usecase-sopimukset.md
  - .backlog/docs/governance/Agenttien päätöksenteon reunaehdot.md
priority: medium
ordinal: 3000
---

## Description

<!-- SECTION:DESCRIPTION:BEGIN -->
### MITÄ
Toteuta Auth-kontekstin public registration ADR-009:n mukaisesti.

- Tarjoa julkinen REST-rajapinta `POST /auth/register`.
- Hyväksy pyynnössä vain `name`, `email` ja `password`.
- Hylkää clientin antamat `role`- ja `enabled`-kentät.
- Tarkista rekisteröinnin feature flag polusta `/feature/auth/register_user`.
- Luo uusi käyttäjä roolilla `READER`, `enabled=true` ja `email_verified_at=null`.
- Hashaa salasana `PasswordHasher`-portilla, tallenna verification-tokenin digest ja julkaise tokeniton `NewUserRegistered`-domain-event.

### MIKSI
Rekisteröinti käynnistää käyttäjän elinkaaren ilman admin-toimenpidettä. Usecase varmistaa, että uusi käyttäjä syntyy yhtenäisillä Auth-säännöillä eikä client voi nostaa oikeuksiaan tai ohittaa sähköpostivahvistusta.
<!-- SECTION:DESCRIPTION:END -->

## Acceptance Criteria
<!-- AC:BEGIN -->
- [ ] #1 GIVEN rekisteröinti on feature flagilla sallittu ja email on uusi, WHEN `POST /auth/register` kutsutaan validilla `name`, `email` ja `password` -pyynnöllä, THEN vastaus on `201 Created` ja käyttäjä persistetään roolilla `READER`, `enabled=true` ja `email_verified_at=null`.
- [ ] #2 GIVEN rekisteröinti onnistuu, WHEN käyttäjä persistetään, THEN tallennettu käyttäjä sisältää password hashin ja verification-token-digestin mutta ei plaintext-salasanaa tai plaintext-tokenia.
- [ ] #3 GIVEN rekisteröinti onnistuu, WHEN `NewUserRegistered` julkaistaan, THEN tapahtuma noudattaa ADR-009:n `DomainEvent`-sopimusta eikä sisällä plaintext-tokenia, token-digestiä, salasanaa tai password hashia.
- [ ] #4 GIVEN pyyntö sisältää `role`- tai `enabled`-kentän, WHEN `POST /auth/register` kutsutaan, THEN pyyntö hylätään validointivirheenä eikä käyttäjää luoda.
- [ ] #5 GIVEN email on jo käytössä, WHEN rekisteröintiä yritetään samalla emaililla, THEN pyyntö hylätään konfliktina eikä uutta käyttäjää tai domain-tapahtumaa synny.
- [ ] #6 GIVEN rekisteröinnin feature flag puuttuu, on lukukelvoton tai on `false`, WHEN `POST /auth/register` kutsutaan, THEN rekisteröinti hylätään hallitulla virheellä eikä käyttäjää persistetä.
- [ ] #7 GIVEN pyynnön email, name tai password ei täytä ADR-009:n sääntöjä, WHEN rekisteröintiä yritetään, THEN pyyntö hylätään validointivirheenä ennen persistointia.
<!-- AC:END -->
## Definition of Done
<!-- DOD:BEGIN -->
- [ ] #1 Käyttäjän määrittelemät Spec by Example -esimerkit on huomioitu toteutuksessa.
- [ ] #2 Toteutus on testattu tehtävän acceptance criteria -kohtia vasten.
- [ ] #3 Toteutuksen lopputulos ja mahdolliset rajaukset on kirjattu Final Summary -osioon.
<!-- DOD:END -->

## Implementation Plan

<!-- SECTION:PLAN:BEGIN -->
Agentti täyttää tähän MITEN tehtävä toteutetaan käyttäjän määrittelemien kohtien MITÄ, MIKSI ja ESIMERKIT perusteella.

- [Toteutustapa]
- [Keskeiset tiedostot, rajapinnat tai komponentit]
- [Testaus- ja varmistustapa]
<!-- SECTION:PLAN:END -->

## Implementation Notes

<!-- SECTION:NOTES:BEGIN -->
Agentti kirjaa tähän toteutuksen aikaiset havainnot, päätökset ja mahdolliset poikkeamat suunnitelmasta.
<!-- SECTION:NOTES:END -->

## Final Summary

<!-- SECTION:FINAL_SUMMARY:BEGIN -->
Agentti kirjaa tähän loppuyhteenvedon, kun tehtävä on valmis.
<!-- SECTION:FINAL_SUMMARY:END -->
