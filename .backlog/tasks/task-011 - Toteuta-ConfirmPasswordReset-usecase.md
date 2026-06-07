---
id: TASK-011
title: 'Auth: Salasanan resetoinnin vahvistus'
status: To Do
assignee: []
created_date: '2026-06-07 08:59'
updated_date: '2026-06-07 12:19'
labels:
  - Backend
  - Auth
milestone: m-1
dependencies:
  - TASK-015
  - TASK-006
references:
  - >-
    .backlog/tasks/task-015 -
    Detail-spec-Auth-domain-API-ja-persistence-contract.md
  - >-
    https://cheatsheetseries.owasp.org/cheatsheets/Forgot_Password_Cheat_Sheet.html
  - >-
    https://cheatsheetseries.owasp.org/cheatsheets/Password_Storage_Cheat_Sheet.html
documentation:
  - .backlog/docs/intent/doc-001 - goal.md
  - .backlog/docs/specs/doc-006 - bounded-context-map-and-glossary.md
priority: medium
ordinal: 5500
---

## Description

<!-- SECTION:DESCRIPTION:BEGIN -->
### MITÄ
Toteuta Auth-kontekstin salasanan resetoinnin vahvistus Auth detail-specin ja tämän tehtävän acceptance criteria -kohtien mukaisesti.

- Käyttäjä voi vahvistaa salasanan resetoinnin kertakäyttöisellä resetointisalaisuudella ja uudella salasanalla.
- Vahvistus onnistuu vain tunnetulle käyttäjälle, jonka resetointisalaisuus on oikea, voimassa ja käyttämätön.
- Onnistunut vahvistus vaihtaa salasanan ja kuluttaa resetointisalaisuuden.
- Virheellinen vahvistus ei vaihda salasanaa eikä paljasta tarkkaa hylkäyksen syytä.
- Salaisuuksia ei palauteta, julkaista tai lokiteta.

### MIKSI
Resetointipyyntö ei yksin vaihda salasanaa. Vahvistuskäyttötapaus viimeistelee kaksivaiheisen palautusvirran kertakäyttöisellä salaisuudella ilman, että plaintext-salaisuutta tai credential-tietoja tallennetaan, julkaistaan tai lokitetaan.
<!-- SECTION:DESCRIPTION:END -->

## Acceptance Criteria
<!-- AC:BEGIN -->
- [ ] #1 GIVEN käyttäjä on olemassa, resetointisalaisuus on oikea, voimassa ja käyttämätön sekä uusi salasana on validi, WHEN resetointi vahvistetaan, THEN salasana vaihdetaan ja resetointisalaisuus kulutetaan.
- [ ] #2 GIVEN resetoinnin vahvistus onnistuu, WHEN käyttäjän salasanatiedot tallennetaan, THEN vain Auth detail-specissä määritetyt salasanan ja resetointisalaisuuden tiedot muuttuvat.
- [ ] #3 GIVEN resetointisalaisuus on väärä, vanhentunut, jo käytetty tai käyttäjää ei löydy, WHEN resetointia vahvistetaan, THEN vahvistus hylätään yhdenmukaisena validointivirheenä eikä salasanaa tai resetointisalaisuuden tilaa muuteta.
- [ ] #4 GIVEN uusi salasana ei täytä hyväksyttyjä validointisääntöjä, WHEN resetointia vahvistetaan, THEN pyyntö hylätään eikä resetointisalaisuutta kuluteta.
- [ ] #5 GIVEN resetoinnin vahvistus onnistuu, WHEN samaa resetointisalaisuutta yritetään käyttää uudelleen, THEN toinen yritys hylätään eikä salasanaa vaihdeta uudelleen.
- [ ] #6 GIVEN resetoinnin vahvistus onnistuu tai epäonnistuu, WHEN vastaus ja lokit muodostetaan, THEN salasanaa, resetointisalaisuutta tai salaisuuden tarkistamiseen käytettyä salattua tietoa ei palauteta tai lokiteta.
<!-- AC:END -->



## Definition of Done
<!-- DOD:BEGIN -->
- [ ] #1 Käyttäjän määrittelemät Spec by Example -esimerkit on huomioitu toteutuksessa.
- [ ] #2 Toteutus on testattu tehtävän acceptance criteria -kohtia vasten.
- [ ] #3 Toteutuksen lopputulos ja mahdolliset rajaukset on kirjattu Final Summary -osioon.
<!-- DOD:END -->
