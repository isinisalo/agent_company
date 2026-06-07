---
id: doc-002
title: TASK-template
type: guide
created_date: '2026-06-06 07:57'
tags:
  - templates
  - task
---

```md
---
id: task-000
title: "Task title tähän"
status: To Do
assignee: []
created_date: 'YYYY-MM-DD HH:mm'
labels: []
milestone: m-0
dependencies: []
priority: medium
ordinal: 1000
---

## Description

<!-- SECTION:DESCRIPTION:BEGIN -->
### MITÄ

Kuvaa konkreettisesti, mitä tehtävän tulee saada aikaan.

- [Täydennä haluttu lopputulos]
- [Täydennä tärkeimmät käyttäjälle tai järjestelmälle näkyvät muutokset]

### MIKSI

Kuvaa, miksi tehtävä on tarpeellinen ja mitä ongelmaa se ratkaisee.

- [Täydennä tausta tai ongelma]
- [Täydennä tavoiteltu hyöty]

<!-- SECTION:DESCRIPTION:END -->

## Acceptance Criteria
<!-- AC:BEGIN -->
- [ ] #1 GIVEN [lähtötilanne], WHEN [toiminto tai tapahtuma], THEN [odotettu lopputulos]
- [ ] #2 GIVEN [lähtötilanne], WHEN [toiminto tai tapahtuma], THEN [odotettu lopputulos]
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
```
