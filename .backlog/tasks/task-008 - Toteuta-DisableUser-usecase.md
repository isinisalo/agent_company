---
id: TASK-008
title: Toteuta DisableUser-usecase
status: To Do
assignee: []
created_date: '2026-06-06 08:19'
updated_date: '2026-06-07 10:08'
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
priority: medium
ordinal: 7000
---

## Description

<!-- SECTION:DESCRIPTION:BEGIN -->
### MITÄ
Toteuta Auth-kontekstin admin-toiminto käyttäjätilin estämiseen.

- Tarjoa REST-rajapinta `PATCH /auth/users/disable`.
- Vaadi auktorisoinniksi `ADMIN`-rooli.
- Hyväksy query-parametrina `email`.
- Lataa käyttäjä normalisoidulla emaililla `IUserRepository`-portin kautta.
- Aseta käyttäjän `enabled=false` ja persistoi päivitys.
- Älä muuta käyttäjän `email_verified_at`-arvoa.

### MIKSI
Adminin pitää pystyä estämään käyttäjätilin API-käyttö ilman tilin poistamista ja ilman, että sähköpostivahvistuksen tila muuttuu. Usecase keskittää käyttöeston Auth-domainiin ja rajaa muutoksen vain `ADMIN`-roolille.
<!-- SECTION:DESCRIPTION:END -->

## Acceptance Criteria
<!-- AC:BEGIN -->
- [ ] #1 GIVEN enabled user ja kutsuja roolilla `ADMIN`, WHEN `PATCH /auth/users/disable?email=...` kutsutaan, THEN vastaus on `204 No Content` ja käyttäjä persistetään `enabled=false`.
- [ ] #2 GIVEN user on jo `enabled=false` ja kutsuja roolilla `ADMIN`, WHEN disable-usecase kutsutaan, THEN vastaus on `204 No Content` ja operaatio on idempotentti.
- [ ] #3 GIVEN käyttäjä löytyy, WHEN disable-usecase onnistuu, THEN `email_verified_at` ei muutu.
- [ ] #4 GIVEN käyttäjää ei löydy ja kutsuja on `ADMIN`, WHEN disable-usecase kutsutaan emaililla, THEN vastaus on `404 Not Found` eikä uutta käyttäjää luoda.
- [ ] #5 GIVEN kutsujan rooli ei ole `ADMIN`, WHEN disable-usecasea kutsutaan, THEN pyyntö hylätään auktorisointivirheenä ennen käyttäjän päivittämistä.
- [ ] #6 GIVEN deaktivointi onnistuu tai epäonnistuu, WHEN vastaus ja lokit muodostetaan, THEN domain-tapahtumia ei julkaista eikä credential- tai token-kenttiä lokiteta.
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
