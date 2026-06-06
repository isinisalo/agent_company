---
id: TASK-009
title: Toteuta DeleteUser-usecase
status: To Do
assignee: []
created_date: '2026-06-06 08:20'
updated_date: '2026-06-06 08:39'
labels:
  - Backend
  - Auth
milestone: m-1
dependencies:
  - TASK-002
priority: medium
ordinal: 8000
---

## Description

<!-- SECTION:DESCRIPTION:BEGIN -->
### MITÄ
Toteuta Auth-kontekstin käyttäjän poisto sähköpostiosoitteella.

- Tarjoa REST-rajapinta `DELETE /auth/users`.
- Vaadi auktorisoinniksi rooli vähintään `ADMIN`.
- Hyväksy query-parametrina `email`.
- Poista käyttäjä `IUserRepository.delete_user`-portin kautta.
- Tee poistosta idempotentti: puuttuva käyttäjä ei aiheuta virhettä.
- Palauta onnistuneesta poistosta no content -vastaus.

### MIKSI
Admin-käyttäjän pitää pystyä poistamaan käyttäjätili järjestelmästä. Idempotentti poisto tekee API-käytöstä vakaampaa ja vastaa määritettyä käyttäytymistä myös silloin, kun käyttäjä on jo poistettu.
<!-- SECTION:DESCRIPTION:END -->

## Acceptance Criteria
<!-- AC:BEGIN -->
- [ ] #1 GIVEN existing user, WHEN `DELETE /auth/users` kutsutaan ADMIN-roolilla ja emaililla, THEN vastaus on `204` ja käyttäjä poistetaan.
- [ ] #2 GIVEN missing user, WHEN `DELETE /auth/users` kutsutaan ADMIN-roolilla ja emaililla, THEN vastaus on `204` eikä virhettä palauteta.
- [ ] #3 GIVEN kutsujan rooli on alle ADMIN, WHEN delete-usecasea kutsutaan, THEN pyyntö hylätään auktorisointivirheenä eikä poistoa tehdä.
- [ ] #4 GIVEN poisto käsitellään, WHEN usecase suoritetaan, THEN käyttäjää ei tarvitse ladata aggregaattina ennen `IUserRepository.delete_user`-kutsua.
- [ ] #5 GIVEN poisto onnistuu tai käyttäjää ei löydy, WHEN vastaus muodostetaan, THEN domain-tapahtumia ei julkaista.
<!-- AC:END -->

## Definition of Done
<!-- DOD:BEGIN -->
- [ ] #1 Käyttäjän määrittelemät Spec by Example -esimerkit on huomioitu toteutuksessa.
- [ ] #2 Toteutus on testattu tehtävän acceptance criteria -kohtia vasten.
- [ ] #3 Toteutuksen lopputulos ja mahdolliset rajaukset on kirjattu Final Summary -osioon.
<!-- DOD:END -->
