---
id: TASK-011
title: Toteuta ConfirmPasswordReset-usecase
status: To Do
assignee: []
created_date: '2026-06-07 08:59'
updated_date: '2026-06-07 09:38'
labels:
  - Backend
  - Auth
milestone: m-1
dependencies:
  - TASK-002
  - TASK-006
references:
  - >-
    .backlog/decisions/*.md
  - .backlog/docs/intent/goal.md
  - .backlog/docs/governance/Agenttien päätöksenteon reunaehdot.md
  - https://cheatsheetseries.owasp.org/cheatsheets/Forgot_Password_Cheat_Sheet.html
  - https://cheatsheetseries.owasp.org/cheatsheets/Password_Storage_Cheat_Sheet.html
priority: medium
ordinal: 5500
---

## Description

<!-- SECTION:DESCRIPTION:BEGIN -->
### MITÄ
Toteuta Auth-kontekstin salasanan resetoinnin vahvistus ADR-009:n mukaisesti.

- Tarjoa julkinen REST-rajapinta `POST /auth/password-resets`.
- Hyväksy pyynnössä `email`, `token` ja `new_password`.
- Lataa käyttäjä normalisoidulla emaililla `IUserRepository`-portista.
- Varmista token käyttäjän `reset_password_token_digest`- ja `reset_password_token_expires_at` -arvoja vasten.
- Validoi ja hash-aa uusi salasana `PasswordHasher`-portilla.
- Päivitä käyttäjän password hash, password hash algorithm, `updated_at`, tyhjennä reset-tokenin digest ja vanhenemisaika, ja persistoi käyttäjä.

### MIKSI
Resetointipyyntö ei yksin vaihda salasanaa. Vahvistususecase viimeistelee kaksivaiheisen palautusvirran kertakäyttöisellä tokenilla ilman, että plaintext-tokenia tai credential-kenttiä tallennetaan, julkaistaan tai lokitetaan.
<!-- SECTION:DESCRIPTION:END -->

## Acceptance Criteria
<!-- AC:BEGIN -->
- [ ] #1 GIVEN olemassa oleva käyttäjä, voimassa oleva reset-token ja validi uusi salasana, WHEN `POST /auth/password-resets` kutsutaan, THEN vastaus on `204 No Content` ja käyttäjän salasana päivitetään.
- [ ] #2 GIVEN reset-vahvistus onnistuu, WHEN käyttäjä persistetään, THEN `password_hash`, `password_hash_algorithm` ja `updated_at` päivittyvät sekä `reset_password_token_digest` ja `reset_password_token_expires_at` tyhjennetään.
- [ ] #3 GIVEN token on väärä, vanhentunut, jo käytetty tai käyttäjää ei löydy, WHEN `POST /auth/password-resets` kutsutaan, THEN vastaus on generic validointivirhe eikä käyttäjän salasanaa tai reset-token-kenttiä muuteta.
- [ ] #4 GIVEN `new_password` ei täytä ADR-009:n Password-sääntöjä, WHEN reset-vahvistusta yritetään, THEN pyyntö hylätään validointivirheenä eikä reset-tokenia tyhjennetä.
- [ ] #5 GIVEN reset-vahvistus onnistuu, WHEN samaa tokenia yritetään käyttää uudelleen, THEN toinen pyyntö hylätään generic validointivirheenä eikä salasanaa vaihdeta uudelleen.
- [ ] #6 GIVEN reset-vahvistus onnistuu tai epäonnistuu, WHEN vastaus ja lokit muodostetaan, THEN domain-tapahtumia ei julkaista eikä salasanaa, password hashia, plaintext-tokenia tai token-digestiä palauteta tai lokiteta.
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
