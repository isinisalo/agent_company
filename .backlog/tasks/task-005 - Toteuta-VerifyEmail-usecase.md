---
id: TASK-005
title: 'Auth: Sähköpostin vahvistus'
status: To Do
assignee: []
created_date: '2026-06-06 08:19'
updated_date: '2026-06-07 11:24'
labels:
  - Backend
  - Auth
milestone: m-1
dependencies:
  - TASK-015
references:
  - >-
    .backlog/tasks/task-015 -
    Detail-spec-Auth-domain-API-ja-persistence-contract.md
documentation:
  - .backlog/docs/intent/doc-001 - goal.md
  - .backlog/docs/governance/Agenttien päätöksenteon reunaehdot.md
  - .backlog/docs/specs/doc-006 - bounded-context-map-and-glossary.md
priority: medium
ordinal: 4000
---

## Description

<!-- SECTION:DESCRIPTION:BEGIN -->
### MITÄ
Toteuta Auth-kontekstin sähköpostin vahvistus Auth detail-specin ja tämän tehtävän acceptance criteria -kohtien mukaisesti.

- Käyttäjä voi vahvistaa sähköpostinsa kertakäyttöisellä vahvistussalaisuudella.
- Vahvistus onnistuu vain tunnetulle käyttäjälle, jonka vahvistussalaisuus on oikea, voimassa ja käyttämätön.
- Onnistunut vahvistus merkitsee sähköpostin vahvistetuksi ja kuluttaa vahvistussalaisuuden.
- Vahvistus ei muuta adminin hallitsemaa käyttötilaa.
- Virheelliset vahvistusyritykset hylätään paljastamatta salaisuuksia.

### MIKSI
Sähköpostivahvistus viimeistelee rekisteröinnin login-kelpoiseksi ilman, että vahvistussalaisuuden plaintext-arvoa tallennetaan tai julkaistaan. Käyttötapaus erottaa sähköpostin vahvistuksen adminin käyttöestoista.
<!-- SECTION:DESCRIPTION:END -->

## Acceptance Criteria
<!-- AC:BEGIN -->
- [ ] #1 GIVEN käyttäjän sähköposti on vahvistamatta ja vahvistussalaisuus on oikea, voimassa ja käyttämätön, WHEN sähköpostia vahvistetaan, THEN sähköposti merkitään vahvistetuksi ja vahvistussalaisuus kulutetaan.
- [ ] #2 GIVEN käyttäjän hallinnollinen käyttötila on sallittu tai estetty, WHEN sähköpostivahvistus onnistuu, THEN hallinnollinen käyttötila ei muutu.
- [ ] #3 GIVEN vahvistussalaisuus on väärä, vanhentunut, jo käytetty tai käyttäjää ei löydy, WHEN sähköpostia vahvistetaan, THEN vahvistus hylätään yhdenmukaisena validointivirheenä eikä käyttäjää muuteta.
- [ ] #4 GIVEN vahvistuspyyntö on puutteellinen tai virheellinen, WHEN sitä käsitellään, THEN se hylätään ennen muutosten tallentamista.
- [ ] #5 GIVEN sähköpostivahvistus onnistuu tai epäonnistuu, WHEN vastaus ja lokit muodostetaan, THEN vahvistussalaisuutta tai sen tarkistamiseen käytettyä salattua tietoa ei palauteta, julkaista tai lokiteta.
<!-- AC:END -->

## Definition of Done
<!-- DOD:BEGIN -->
- [ ] #1 Käyttäjän määrittelemät Spec by Example -esimerkit on huomioitu toteutuksessa.
- [ ] #2 Toteutus on testattu tehtävän acceptance criteria -kohtia vasten.
- [ ] #3 Toteutuksen lopputulos ja mahdolliset rajaukset on kirjattu Final Summary -osioon.
<!-- DOD:END -->
