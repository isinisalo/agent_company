---
id: TASK-012
title: 'Auth: tietokantarakennepäätös'
status: To Do
assignee: []
created_date: '2026-06-07 10:34'
labels:
  - Backend
  - Auth
milestone: m-1
dependencies: []
references:
  - .backlog/decisions/*.md
  - .backlog/docs/intent/goal.md
  - .backlog/docs/governance/Agenttien päätöksenteon reunaehdot.md
priority: medium
ordinal: 1000
---

## Description

<!-- SECTION:DESCRIPTION:BEGIN -->
### MITÄ
Suunnittele Auth bounded contextin tietokantarakenne ja kirjaa päätös ADR-dokumentiksi.

Päätöksen pitää kuvata, miten Authin käyttäjä-, kirjautumis-, sähköpostivahvistus-, salasanan resetointi-, hallinta- ja listauskäyttötapaukset voidaan toteuttaa valitulla tietokantaratkaisulla ilman, että käyttötapaustaskit lukitsevat tietomallia.

### MIKSI
Käyttötapausten toteutus on suoraviivaisempaa, kun tallennettava tieto, hakutarpeet, salaisuuksien käsittely ja poistokäyttäytyminen on päätetty ennen yksittäisten käyttötapausten rakentamista.
<!-- SECTION:DESCRIPTION:END -->

## Acceptance Criteria
<!-- AC:BEGIN -->
- [ ] #1 GIVEN Authin tietokantarakenne suunnitellaan, WHEN tehtävä valmistuu, THEN `.backlog/decisions` sisältää uuden Auth-tietokantaa koskevan ADR-dokumentin.
- [ ] #2 GIVEN ADR kirjoitetaan, WHEN dokumentti tarkistetaan, THEN se noudattaa nykyistä `Context`, `Decision` ja `Consequences` -rakennetta.
- [ ] #3 GIVEN päätös luetaan käyttötapausten toteutusta varten, WHEN kirjautumisen, rekisteröinnin, sähköpostivahvistuksen, salasanan resetoinnin, käyttäjähallinnan ja listauksen tarpeet arvioidaan, THEN päätös kattaa niiden tarvitsemat tallennus- ja hakutarpeet käyttötapaustasolla.
- [ ] #4 GIVEN päätös käsittelee Authin salaisia tietoja, WHEN seuraukset kirjataan, THEN salasanojen, tokenien, digestien ja muiden credential-luonteisten tietojen tallennus- ja vuotamattomuusrajaukset ovat eksplisiittiset.
- [ ] #5 GIVEN ADR hyväksytään, WHEN käyttötapaustaskit toteutetaan myöhemmin, THEN ne voivat viitata ADR:ään tietokantarakenteen lähteenä ilman omia tietomallipäätöksiä.
<!-- AC:END -->
