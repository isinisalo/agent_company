---
id: TASK-010
title: Toteuta ListUsers-usecase
status: To Do
assignee: []
created_date: '2026-06-06 08:20'
updated_date: '2026-06-07 09:38'
labels:
  - Backend
  - Auth
milestone: m-1
dependencies:
  - TASK-002
references:
  - >-
    .backlog/decisions/*.md
  - .backlog/docs/intent/goal.md
  - .backlog/docs/governance/Agenttien päätöksenteon reunaehdot.md
priority: medium
ordinal: 9000
---

## Description

<!-- SECTION:DESCRIPTION:BEGIN -->
### MITÄ
Toteuta Auth-kontekstin admin-listaus käyttäjäsummaryille ADR-009:n mukaisesti.

- Tarjoa REST-rajapinta `GET /auth/users`.
- Vaadi auktorisoinniksi `ADMIN`-rooli.
- Hyväksy valinnaiset query-parametrit `limit` ja `cursor`.
- Hae käyttäjäsummary-sivu `IUserRepository.list_users(limit, cursor)`-portin kautta ilman runtime-tauluskannausta.
- Palauta tyhjä lista, kun käyttäjiä ei ole.
- Älä palauta credential-, password hash- tai token-digest-kenttiä.

### MIKSI
Admin-käyttäjän pitää pystyä tarkastelemaan käyttäjiä hallintaa varten ilman, että Authin salaiset tai credential-luonteiset kentät vuotavat API-vastaukseen. Rajattu ja sivutettu listaus sopii DynamoDB:n access pattern -reunaehtoihin paremmin kuin rajoittamaton tauluskannaus.
<!-- SECTION:DESCRIPTION:END -->

## Acceptance Criteria
<!-- AC:BEGIN -->
- [ ] #1 GIVEN users exist ja kutsuja roolilla `ADMIN`, WHEN `GET /auth/users` kutsutaan, THEN vastaus on `200 OK` ja sisältää käyttäjäsummaryjen listan.
- [ ] #2 GIVEN no users ja kutsuja roolilla `ADMIN`, WHEN `GET /auth/users` kutsutaan, THEN vastaus on `200 OK` ja sisältää tyhjän listan.
- [ ] #3 GIVEN kutsujan rooli ei ole `ADMIN`, WHEN list-users-usecasea kutsutaan, THEN pyyntö hylätään auktorisointivirheenä ennen käyttäjien hakua.
- [ ] #4 GIVEN listaus suoritetaan, WHEN käyttäjät haetaan, THEN käytetään `IUserRepository.list_users(limit, cursor)`-porttia eikä käyttäjiä persistetä.
- [ ] #5 GIVEN vastaus muodostetaan, WHEN käyttäjäsummaryt serialisoidaan, THEN yksikään item ei sisällä `password_hash`, `password_hash_algorithm`, `verification_token_digest`, `reset_password_token_digest`, plaintext-tokenia tai muuta credential-kenttää.
- [ ] #6 GIVEN `limit` puuttuu tai ylittää sallitun ylärajan, WHEN listaus suoritetaan, THEN käytetään toteutuksessa määriteltyä turvallista oletus- tai maksimiarvoa ja palautetaan `next_cursor`, jos lisää tuloksia on saatavilla.
- [ ] #7 GIVEN listaus onnistuu, WHEN vastaus ja lokit muodostetaan, THEN domain-tapahtumia ei julkaista eikä credential- tai token-kenttiä lokiteta.
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
