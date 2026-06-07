---
id: TASK-004
title: 'Auth: Käyttäjän rekisteröinti'
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
ordinal: 3000
---

## Description

<!-- SECTION:DESCRIPTION:BEGIN -->
### MITÄ
Toteuta Auth-kontekstin käyttäjän rekisteröinti Auth detail-specin ja tämän tehtävän acceptance criteria -kohtien mukaisesti.

- Uusi käyttäjä voi rekisteröityä, kun rekisteröinti on järjestelmän asetuksilla sallittu.
- Rekisteröityvä käyttäjä syntyy perusoikeuksilla, käyttöön sallittuna ja sähköposti vahvistamattomana, ellei Auth detail-spec määritä turvallisempaa rajaa.
- Rekisteröityvä käyttäjä ei voi itse valita rooliaan tai hallinnollista käyttötilaansa.
- Onnistunut rekisteröinti käynnistää sähköpostivahvistuksen ilman salaisuuksien vuotamista.
- Rekisteröinti hylätään, jos käyttäjän tunniste on jo käytössä tai syöte ei täytä hyväksyttyjä sääntöjä.

### MIKSI
Rekisteröinti käynnistää käyttäjän elinkaaren ilman admin-toimenpidettä. Käyttötapaus varmistaa, että uusi käyttäjä syntyy yhtenäisillä Auth-säännöillä eikä client voi nostaa oikeuksiaan tai ohittaa sähköpostivahvistusta.
<!-- SECTION:DESCRIPTION:END -->

## Acceptance Criteria
<!-- AC:BEGIN -->
- [ ] #1 GIVEN rekisteröinti on sallittu ja käyttäjän tunniste on vapaa, WHEN käyttäjä rekisteröityy validilla nimellä, yhteystiedolla ja salasanalla, THEN käyttäjä luodaan perusoikeuksilla, käyttöön sallittuna ja sähköpostivahvistusta odottavana.
- [ ] #2 GIVEN rekisteröinti onnistuu, WHEN käyttäjään liittyvät salaisuudet käsitellään, THEN plaintext-salasanaa tai sähköpostivahvistuksen salaisuutta ei tallenneta, palauteta, julkaista tai lokiteta.
- [ ] #3 GIVEN rekisteröityvä käyttäjä yrittää valita roolin tai hallinnollisen käyttötilan, WHEN rekisteröintiä käsitellään, THEN pyyntö hylätään eikä käyttäjää luoda.
- [ ] #4 GIVEN käyttäjän tunniste on jo käytössä, WHEN rekisteröintiä yritetään samalla tunnisteella, THEN pyyntö hylätään eikä uutta käyttäjää tai rekisteröintisignaalia synny.
- [ ] #5 GIVEN rekisteröintiä ei ole järjestelmän asetuksilla sallittu tai asetusta ei voi tulkita turvallisesti, WHEN rekisteröintiä yritetään, THEN rekisteröinti hylätään eikä käyttäjää luoda.
- [ ] #6 GIVEN nimi, yhteystieto tai salasana ei täytä hyväksyttyjä validointisääntöjä, WHEN rekisteröintiä yritetään, THEN pyyntö hylätään ennen käyttäjän luomista.
<!-- AC:END -->

## Definition of Done
<!-- DOD:BEGIN -->
- [ ] #1 Käyttäjän määrittelemät Spec by Example -esimerkit on huomioitu toteutuksessa.
- [ ] #2 Toteutus on testattu tehtävän acceptance criteria -kohtia vasten.
- [ ] #3 Toteutuksen lopputulos ja mahdolliset rajaukset on kirjattu Final Summary -osioon.
<!-- DOD:END -->
