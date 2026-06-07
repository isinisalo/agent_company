---
id: TASK-006
title: 'Auth: Salasanan resetointipyyntö'
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
  - >-
    https://cheatsheetseries.owasp.org/cheatsheets/Forgot_Password_Cheat_Sheet.html
documentation:
  - .backlog/docs/intent/goal.md
  - .backlog/docs/governance/Agenttien päätöksenteon reunaehdot.md
  - .backlog/docs/specs/doc-006 - bounded-context-map-and-glossary.md
priority: medium
ordinal: 5000
---

## Description

<!-- SECTION:DESCRIPTION:BEGIN -->
### MITÄ
Toteuta Auth-kontekstin salasanan resetointipyyntö Auth detail-specin ja tämän tehtävän acceptance criteria -kohtien mukaisesti.

- Käyttäjä voi pyytää salasanan resetointia tunnisteensa perusteella.
- Resetointipyyntö ei paljasta, onko tunnisteella käyttäjää.
- Tunnetulle käyttäjälle syntyy kertakäyttöinen resetointisalaisuus, joka voidaan toimittaa hyväksytyn viestintäpolun kautta.
- Salaisuudesta ei tallenneta, palauteta, julkaista tai lokiteta plaintext-arvoa.
- Virheellinen syöte hylätään ennen käyttäjähakua.

### MIKSI
Salasanan resetointipyyntö käynnistää palautusvirran ilman käyttäjän olemassaolon paljastamista. Käyttötapaus varmistaa, että resetointisalaisuus käsitellään turvallisesti ja että varsinainen salasanan vaihto tapahtuu erillisessä vahvistusvaiheessa.
<!-- SECTION:DESCRIPTION:END -->

## Acceptance Criteria
<!-- AC:BEGIN -->
- [ ] #1 GIVEN tunnettu käyttäjä ja validi resetointipyyntö, WHEN salasanan resetointia pyydetään, THEN pyyntö hyväksytään ja resetointisalaisuus voidaan toimittaa hyväksytyn viestintäpolun kautta.
- [ ] #2 GIVEN tunnettu käyttäjä, WHEN resetointipyyntö hyväksytään, THEN vain Auth detail-specissä määritetty salaisuuden tarkistamiseen tarvittava tieto tallennetaan eikä plaintext-salaisuutta tallenneta.
- [ ] #3 GIVEN tuntematon käyttäjän tunniste, WHEN salasanan resetointia pyydetään, THEN lopputulos ei paljasta käyttäjän puuttumista eikä uutta käyttäjää luoda.
- [ ] #4 GIVEN resetointipyyntö on puutteellinen tai virheellinen, WHEN sitä käsitellään, THEN se hylätään ennen käyttäjähakua.
- [ ] #5 GIVEN resetointipyyntö onnistuu tai käyttäjää ei löydy, WHEN vastaus ja lokit muodostetaan, THEN käyttäjän olemassaoloa, resetointisalaisuutta tai salaisuuden tarkistamiseen käytettyä salattua tietoa ei palauteta tai lokiteta.
<!-- AC:END -->



## Definition of Done
<!-- DOD:BEGIN -->
- [ ] #1 Käyttäjän määrittelemät Spec by Example -esimerkit on huomioitu toteutuksessa.
- [ ] #2 Toteutus on testattu tehtävän acceptance criteria -kohtia vasten.
- [ ] #3 Toteutuksen lopputulos ja mahdolliset rajaukset on kirjattu Final Summary -osioon.
<!-- DOD:END -->
