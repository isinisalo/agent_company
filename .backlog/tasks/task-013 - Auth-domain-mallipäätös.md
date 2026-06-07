---
id: TASK-013
title: 'Auth: domain-mallipäätös'
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
ordinal: 1100
---

## Description

<!-- SECTION:DESCRIPTION:BEGIN -->
### MITÄ
Suunnittele Auth bounded contextin yhteinen domain-malli ja kirjaa päätös ADR-dokumentiksi.

Päätöksen pitää kuvata Authin käyttäjäidentiteetti, käyttäjän elinkaaren tilat, roolit, kirjautumiskelpoisuus, salasanakäsittelyn periaatteet, kertakäyttöisten vahvistusten periaatteet ja tapahtumien tietoturvarajat käyttötapaustasolla.

### MIKSI
Yksittäiset käyttötapaukset eivät saa päättää samaa domain-kieltä ja samoja invariansseja eri tavoin. Yhteinen päätös vähentää päällekkäistä mallinnusta ja estää ristiriitaiset Auth-säännöt.
<!-- SECTION:DESCRIPTION:END -->

## Acceptance Criteria
<!-- AC:BEGIN -->
- [ ] #1 GIVEN Authin domain-malli suunnitellaan, WHEN tehtävä valmistuu, THEN `.backlog/decisions` sisältää uuden Auth-domainia koskevan ADR-dokumentin.
- [ ] #2 GIVEN ADR kirjoitetaan, WHEN dokumentti tarkistetaan, THEN se noudattaa nykyistä `Context`, `Decision` ja `Consequences` -rakennetta.
- [ ] #3 GIVEN käyttötapaukset tarvitsevat yhteistä domain-kieltä, WHEN päätöstä luetaan, THEN käyttäjäidentiteetti, roolit, käyttäjän elinkaaren tilat ja kirjautumiskelpoisuuden säännöt on kuvattu ilman kooditason luokka- tai rajapintanimiä.
- [ ] #4 GIVEN Auth käsittelee salasanoja ja kertakäyttöisiä vahvistuksia, WHEN seuraukset kirjataan, THEN päätös määrittää turvallisen käsittelyn periaatteet ja salaisuuksien vuotamattomuusrajat.
- [ ] #5 GIVEN ADR hyväksytään, WHEN käyttötapaustaskit toteutetaan myöhemmin, THEN ne voivat viitata ADR:ään domain-mallin lähteenä ilman omia domain-rakennemäärityksiä.
<!-- AC:END -->
