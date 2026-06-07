---
id: TASK-014
title: 'Auth: REST-rajapintapäätös'
status: Done
assignee: []
created_date: '2026-06-07 10:34'
updated_date: '2026-06-07 10:56'
labels:
  - Backend
  - Auth
milestone: m-1
dependencies: []
references:
  - .backlog/decisions/*.md
  - .backlog/docs/intent/goal.md
  - .backlog/docs/governance/Agenttien päätöksenteon reunaehdot.md
  - .backlog/decisions/decision-011 - Backend-Valitaan-Auth-REST-API-sopimus.md
modified_files:
  - .backlog/decisions/decision-011 - Backend-Valitaan-Auth-REST-API-sopimus.md
priority: medium
ordinal: 1200
---

## Description

<!-- SECTION:DESCRIPTION:BEGIN -->
### MITÄ
Suunnittele Auth bounded contextin REST API -rajapinta ja kirjaa päätös ADR-dokumentiksi.

Päätöksen pitää kuvata kirjautumisen, rekisteröinnin, sähköpostivahvistuksen, salasanan resetoinnin ja admin-käyttäjähallinnan ulkoinen API-sopimus niin, että käyttötapaustaskit voivat jäädä endpoint- ja kenttänimistä riippumattomiksi.

### MIKSI
Rajapinnan polut, metodit, vasteet, validointivirheet ja auktorisointimalli pitää päättää yhtenä kokonaisuutena ennen käyttötapausten toteutusta, jotta API pysyy johdonmukaisena ja turvallisena.
<!-- SECTION:DESCRIPTION:END -->

## Acceptance Criteria
<!-- AC:BEGIN -->
- [x] #1 GIVEN Authin REST-rajapinta suunnitellaan, WHEN tehtävä valmistuu, THEN `.backlog/decisions` sisältää uuden Auth REST API:a koskevan ADR-dokumentin.
- [x] #2 GIVEN ADR kirjoitetaan, WHEN dokumentti tarkistetaan, THEN se noudattaa nykyistä `Context`, `Decision` ja `Consequences` -rakennetta.
- [x] #3 GIVEN päätös kattaa Authin ulkoiset käyttötapaukset, WHEN dokumenttia luetaan, THEN kirjautumisen, rekisteröinnin, sähköpostivahvistuksen, salasanan resetoinnin ja admin-käyttäjähallinnan rajapintaperiaatteet on päätetty yhtenäisesti.
- [x] #4 GIVEN rajapinta käsittelee virhetilanteita, WHEN seuraukset kirjataan, THEN validointi-, auktorisointi-, tunnistautumis- ja tietovuotorajaukset ovat eksplisiittiset.
- [x] #5 GIVEN ADR hyväksytään, WHEN käyttötapaustaskit toteutetaan myöhemmin, THEN ne voivat viitata ADR:ään API-sopimuksen lähteenä ilman omia endpoint- tai kenttänimipäätöksiä.
<!-- AC:END -->

## Final Summary

<!-- SECTION:FINAL_SUMMARY:BEGIN -->
Auth REST API -ADR luotu ja hyväksytty tiedostoon `.backlog/decisions/decision-011 - Backend-Valitaan-Auth-REST-API-sopimus.md`. Päätös lukitsee `/api/v1`-juuren, auth- ja admin-endpointit, request/response-mallit, virheformaatin, authn/authz-rajat, CORS-periaatteen ja HS256 JWT -claim-sopimuksen. Refresh tokenit, revokointi, MFA ja sessiohallinta rajattiin pois tästä päätöksestä.
<!-- SECTION:FINAL_SUMMARY:END -->
