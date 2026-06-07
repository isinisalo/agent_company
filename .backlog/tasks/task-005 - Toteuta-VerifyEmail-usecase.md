---
id: TASK-005
title: Toteuta VerifyEmail-usecase
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
documentation:
  - >-
    .backlog/decisions/decision-009-[Backend]-Määritetään-Auth-bounded-context-ja-usecase-sopimukset.md
  - .backlog/docs/governance/Agenttien päätöksenteon reunaehdot.md
priority: medium
ordinal: 4000
---

## Description

<!-- SECTION:DESCRIPTION:BEGIN -->
### MITÄ
Toteuta Auth-kontekstin sähköpostivahvistus ADR-009:n mukaisesti.

- Tarjoa julkinen REST-rajapinta `POST /auth/email-verifications`.
- Hyväksy pyynnössä `email` ja `token`.
- Lataa käyttäjä normalisoidulla emaililla `IUserRepository`-portista.
- Varmista token käyttäjän `verification_token_digest`- ja `verification_token_expires_at` -arvoja vasten.
- Aseta `email_verified_at`, tyhjennä verification-tokenin digest ja vanhenemisaika, ja persistoi käyttäjä.
- Älä muuta käyttäjän adminin hallitsemaa `enabled`-tilaa.

### MIKSI
Sähköpostivahvistus viimeistelee rekisteröinnin login-kelpoiseksi ilman, että sähköpostitokenin plaintext-arvoa tallennetaan tai julkaistaan. Usecase erottaa sähköpostin vahvistuksen adminin käyttöestoista.
<!-- SECTION:DESCRIPTION:END -->

## Acceptance Criteria
<!-- AC:BEGIN -->
- [ ] #1 GIVEN käyttäjä on vahvistamatta ja token täsmää voimassa olevaan verification-token-digestiin, WHEN `POST /auth/email-verifications` kutsutaan, THEN vastaus on `200 OK`, `email_verified_at` asetetaan ja verification-tokenin digest sekä vanhenemisaika tyhjennetään.
- [ ] #2 GIVEN käyttäjän `enabled` on `true` tai `false`, WHEN sähköpostivahvistus onnistuu, THEN usecase ei muuta `enabled`-arvoa.
- [ ] #3 GIVEN token on väärä, vanhentunut, jo käytetty tai käyttäjää ei löydy, WHEN `POST /auth/email-verifications` kutsutaan, THEN vahvistus hylätään generic validointivirheenä eikä käyttäjää päivitetä.
- [ ] #4 GIVEN pyyntö ei sisällä validia emailia tai tokenia, WHEN `POST /auth/email-verifications` kutsutaan, THEN pyyntö hylätään validointivirheenä ennen persistointia.
- [ ] #5 GIVEN sähköpostivahvistus onnistuu tai epäonnistuu, WHEN vastaus ja lokit muodostetaan, THEN domain-tapahtumia ei julkaista eikä plaintext-tokenia tai token-digestiä palauteta tai lokiteta.
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
