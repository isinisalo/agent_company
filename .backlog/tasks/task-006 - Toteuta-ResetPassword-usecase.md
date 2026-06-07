---
id: TASK-006
title: Toteuta RequestPasswordReset-usecase
status: To Do
assignee: []
created_date: '2026-06-06 08:19'
updated_date: '2026-06-07 10:09'
labels:
  - Backend
  - Auth
milestone: m-1
dependencies:
  - TASK-002
references:
  - .backlog/decisions/*.md
  - .backlog/docs/intent/goal.md
  - .backlog/docs/governance/Agenttien päätöksenteon reunaehdot.md
  - >-
    https://cheatsheetseries.owasp.org/cheatsheets/Forgot_Password_Cheat_Sheet.html
priority: medium
ordinal: 5000
---

## Description

<!-- SECTION:DESCRIPTION:BEGIN -->
### MITÄ
Toteuta Auth-kontekstin salasanan resetointipyynnön aloitus.

- Tarjoa julkinen REST-rajapinta `POST /auth/password-reset-requests`.
- Hyväksy pyynnössä `email`.
- Palauta sama ulkoinen vastaus riippumatta siitä, löytyykö käyttäjää.
- Jos käyttäjä löytyy, luo kertakäyttöinen reset-token, tallenna vain token-digest ja vanhenemisaika käyttäjälle, ja persistoi päivitys.
- Julkaise olemassa olevalle käyttäjälle tokeniton `PasswordResetRequested`-domain-event.
- Älä lukitse käyttäjätiliä resetointipyynnön seurauksena.

### MIKSI
Resetointipyynnön pitää mahdollistaa tilin palautus ilman kirjautumista mutta estää käyttäjätilien enumerointi. Usecase käynnistää reset-virran ja rajaa varsinaisen salasanan vaihtamisen erilliseen `ConfirmPasswordReset`-usecaseen.
<!-- SECTION:DESCRIPTION:END -->

## Acceptance Criteria
<!-- AC:BEGIN -->
- [ ] #1 GIVEN olemassa oleva käyttäjä, WHEN `POST /auth/password-reset-requests` kutsutaan validilla emaililla, THEN vastaus on `202 Accepted` ja sisältää vain generic vastaanotettu -tilan.
- [ ] #2 GIVEN olemassa oleva käyttäjä, WHEN resetointipyyntö hyväksytään, THEN käyttäjälle tallennetaan `reset_password_token_digest` ja `reset_password_token_expires_at` sekä päivitys persistetään `IUserRepository.update`-portin kautta.
- [ ] #3 GIVEN olemassa oleva käyttäjä, WHEN `PasswordResetRequested` julkaistaan, THEN tapahtuma on tokeniton ja credential-vapaa eikä sisällä plaintext-tokenia, token-digestiä, salasanaa tai password hashia.
- [ ] #4 GIVEN tuntematon email, WHEN `POST /auth/password-reset-requests` kutsutaan, THEN vastaus on sama `202 Accepted` ja sama response shape kuin olemassa olevalle käyttäjälle eikä käyttäjää persistetä.
- [ ] #5 GIVEN pyyntö ei sisällä validia emailia, WHEN resetointipyyntöä yritetään, THEN pyyntö hylätään validointivirheenä ennen käyttäjähakua.
- [ ] #6 GIVEN resetointipyyntö onnistuu tai käyttäjää ei löydy, WHEN vastaus ja lokit muodostetaan, THEN järjestelmä ei paljasta käyttäjän olemassaoloa eikä palauta tai lokita plaintext-tokenia tai token-digestiä.
<!-- AC:END -->



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

## Definition of Done
<!-- DOD:BEGIN -->
- [ ] #1 Käyttäjän määrittelemät Spec by Example -esimerkit on huomioitu toteutuksessa.
- [ ] #2 Toteutus on testattu tehtävän acceptance criteria -kohtia vasten.
- [ ] #3 Toteutuksen lopputulos ja mahdolliset rajaukset on kirjattu Final Summary -osioon.
<!-- DOD:END -->
