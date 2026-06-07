---
id: TASK-009
title: Toteuta DeleteUser-usecase
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
ordinal: 8000
---

## Description

<!-- SECTION:DESCRIPTION:BEGIN -->
### MITÄ
Toteuta Auth-kontekstin admin-toiminto käyttäjän poistamiseen sähköpostiosoitteella ADR-009:n mukaisesti.

- Tarjoa REST-rajapinta `DELETE /auth/users`.
- Vaadi auktorisoinniksi `ADMIN`-rooli.
- Hyväksy query-parametrina `email`.
- Poista käyttäjä idempotentisti `IUserRepository.delete_by_email`-portin kautta.
- Rajaa poisto Auth-käyttäjädataan ja credential-/token-digest-kenttiin.
- Palauta onnistuneesta tai jo toteutuneesta poistosta no content -vastaus.

### MIKSI
Adminin pitää pystyä poistamaan Auth-käyttäjätili järjestelmästä. Idempotentti poisto tekee API:sta vakaan myös uudelleenyrityksissä, mutta audit-, privacy- ja laajemmat datanpoistopolitiikat vaativat erillisen päätöksen ennen tuotantolaajennusta.
<!-- SECTION:DESCRIPTION:END -->

## Acceptance Criteria
<!-- AC:BEGIN -->
- [ ] #1 GIVEN existing user ja kutsuja roolilla `ADMIN`, WHEN `DELETE /auth/users?email=...` kutsutaan, THEN vastaus on `204 No Content` ja Auth-käyttäjä poistetaan `IUserRepository.delete_by_email`-portin kautta.
- [ ] #2 GIVEN missing user ja kutsuja roolilla `ADMIN`, WHEN `DELETE /auth/users?email=...` kutsutaan, THEN vastaus on `204 No Content` eikä virhettä palauteta.
- [ ] #3 GIVEN kutsujan rooli ei ole `ADMIN`, WHEN delete-usecasea kutsutaan, THEN pyyntö hylätään auktorisointivirheenä eikä poistoa tehdä.
- [ ] #4 GIVEN poisto käsitellään, WHEN usecase suoritetaan, THEN käyttäjää ei tarvitse ladata aggregaattina ennen `delete_by_email`-kutsua.
- [ ] #5 GIVEN poisto toteutetaan, WHEN sen scopea arvioidaan, THEN taski poistaa vain Auth bounded contextin käyttäjä-, credential- ja token-digest-datan eikä määritä audit-retentiota, anonymisointia tai muiden bounded contextien datapoistoa.
- [ ] #6 GIVEN poisto onnistuu tai käyttäjää ei löydy, WHEN vastaus ja lokit muodostetaan, THEN domain-tapahtumia ei julkaista eikä credential- tai token-kenttiä lokiteta.
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
