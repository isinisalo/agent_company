---
id: TASK-003
title: 'Auth: Kirjautuminen'
status: To Do
assignee: []
created_date: '2026-06-06 08:18'
updated_date: '2026-06-07 10:57'
labels:
  - Backend
  - Auth
milestone: m-1
dependencies:
  - TASK-012
  - TASK-013
  - TASK-014
references:
  - .backlog/decisions/*.md
  - .backlog/docs/intent/goal.md
  - .backlog/docs/governance/Agenttien päätöksenteon reunaehdot.md
  - .backlog/decisions/decision-009 - Backend-Valitaan-Auth-domain-malli.md
  - >-
    .backlog/decisions/decision-010 -
    Data-Valitaan-Auth-DynamoDB-tietokantarakenne.md
  - .backlog/decisions/decision-011 - Backend-Valitaan-Auth-REST-API-sopimus.md
priority: medium
ordinal: 2000
---

## Description

<!-- SECTION:DESCRIPTION:BEGIN -->
### MITÄ
Toteuta Auth-kontekstin käyttäjän kirjautuminen hyväksyttyjen Auth-päätösten mukaisesti.

- Käyttäjä voi kirjautua tunnisteellaan ja salasanallaan.
- Kirjautuminen onnistuu vain, kun käyttäjä tunnetaan, salasana täsmää, sähköposti on vahvistettu ja käyttäjän käyttö on sallittu.
- Epäonnistunut kirjautuminen hylätään yhdenmukaisesti ilman, että tarkka syy paljastuu.
- Onnistunut kirjautuminen tuottaa käyttöoikeustunnisteen ja päivittää kirjautumiseen liittyvät tiedot hyväksyttyjen päätösten mukaisesti.
- Salaisuuksia ei palauteta, julkaista tai lokiteta.

### MIKSI
Kirjautuminen on selaimen ja API:n perusvirta. Käyttötapaus varmistaa, että käyttöoikeustunnisteen saa vain tunnettu, sähköpostinsa vahvistanut ja adminin sallima käyttäjä ilman käyttäjätilin olemassaolon tai tilan vuotamista.
<!-- SECTION:DESCRIPTION:END -->

## Acceptance Criteria
<!-- AC:BEGIN -->
- [ ] #1 GIVEN käyttöön sallittu ja sähköpostinsa vahvistanut käyttäjä sekä oikea salasana, WHEN käyttäjä kirjautuu, THEN kirjautuminen hyväksytään ja käyttäjä saa käyttöoikeustunnisteen.
- [ ] #2 GIVEN tunniste on tuntematon, salasana on väärä, käyttäjän käyttö on estetty tai sähköposti on vahvistamatta, WHEN kirjautumista yritetään, THEN kirjautuminen hylätään samalla tavalla ilman tarkkaa syytä.
- [ ] #3 GIVEN kirjautuminen onnistuu, WHEN kirjautumisen jälkeiset tiedot tallennetaan, THEN vain hyväksytyissä Auth-päätöksissä määritetyt kirjautumistiedot muuttuvat.
- [ ] #4 GIVEN kirjautumispyyntö on puutteellinen tai virheellinen, WHEN sitä käsitellään, THEN se hylätään ennen salasanatarkistusta.
- [ ] #5 GIVEN kirjautuminen onnistuu tai epäonnistuu, WHEN vastaus ja lokit muodostetaan, THEN salasanaa, salasanan tarkistamiseen käytettyjä salaisia tietoja, käyttöoikeustunnisteita tai avaimia ei palauteta tai lokiteta.
<!-- AC:END -->

## Definition of Done
<!-- DOD:BEGIN -->
- [ ] #1 Käyttäjän määrittelemät Spec by Example -esimerkit on huomioitu toteutuksessa.
- [ ] #2 Toteutus on testattu tehtävän acceptance criteria -kohtia vasten.
- [ ] #3 Toteutuksen lopputulos ja mahdolliset rajaukset on kirjattu Final Summary -osioon.
<!-- DOD:END -->
