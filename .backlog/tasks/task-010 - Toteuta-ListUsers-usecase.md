---
id: TASK-010
title: 'Auth: Käyttäjien listaus'
status: To Do
assignee: []
created_date: '2026-06-06 08:20'
updated_date: '2026-06-07 11:25'
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
ordinal: 9000
---

## Description

<!-- SECTION:DESCRIPTION:BEGIN -->
### MITÄ
Toteuta Auth-kontekstin admin-listaus käyttäjäsummaryille Auth detail-specin ja tämän tehtävän acceptance criteria -kohtien mukaisesti.

- Vain hallintakäyttäjä voi listata käyttäjiä.
- Listaus palauttaa rajatun ja sivutettavan käyttäjäsummaryn.
- Tyhjä käyttäjäjoukko palautetaan tyhjänä listana.
- Summary ei sisällä credential-, salasana- tai vahvistussalaisuuksiin liittyviä tietoja.
- Salaisuuksia ei palauteta, julkaista tai lokiteta.

### MIKSI
Admin-käyttäjän pitää pystyä tarkastelemaan käyttäjiä hallintaa varten ilman, että Authin salaiset tai credential-luonteiset tiedot vuotavat. Rajattu ja sivutettava listaus pitää toiminnon hallittavana myös käyttäjämäärän kasvaessa.
<!-- SECTION:DESCRIPTION:END -->

## Acceptance Criteria
<!-- AC:BEGIN -->
- [ ] #1 GIVEN käyttäjiä on olemassa ja kutsuja on hallintakäyttäjä, WHEN käyttäjiä listataan, THEN toiminto palauttaa käyttäjäsummaryjen listan.
- [ ] #2 GIVEN käyttäjiä ei ole ja kutsuja on hallintakäyttäjä, WHEN käyttäjiä listataan, THEN toiminto palauttaa tyhjän listan.
- [ ] #3 GIVEN kutsuja ei ole hallintakäyttäjä, WHEN käyttäjiä yritetään listata, THEN toiminto hylätään ennen käyttäjien hakua.
- [ ] #4 GIVEN käyttäjäsummary muodostetaan, WHEN listauksen tulos palautetaan, THEN yksikään käyttäjäsummary ei sisällä credential-, salasana- tai vahvistussalaisuuksiin liittyviä tietoja.
- [ ] #5 GIVEN sivutuksen koko puuttuu tai ylittää hyväksytyn ylärajan, WHEN listaus suoritetaan, THEN käytetään Auth detail-specissä määritettyä turvallista oletusta tai enimmäiskokoa ja ilmoitetaan, jos lisää tuloksia on saatavilla.
- [ ] #6 GIVEN listaus onnistuu, WHEN vastaus ja lokit muodostetaan, THEN credential- tai vahvistussalaisuuksia ei palauteta, julkaista tai lokiteta.
<!-- AC:END -->



## Definition of Done
<!-- DOD:BEGIN -->
- [ ] #1 Käyttäjän määrittelemät Spec by Example -esimerkit on huomioitu toteutuksessa.
- [ ] #2 Toteutus on testattu tehtävän acceptance criteria -kohtia vasten.
- [ ] #3 Toteutuksen lopputulos ja mahdolliset rajaukset on kirjattu Final Summary -osioon.
<!-- DOD:END -->
