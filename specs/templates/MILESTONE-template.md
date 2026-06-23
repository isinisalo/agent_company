---
id: doc-003
title: MILESTONE-template
type: guide
created_date: '2026-06-06 07:57'
tags:
  - templates
  - milestone
---

```md
---
id: m-0
title: "Milestone nimi tähän"
status: planned
goals: []
adrs: []
non_goals: []
constraints: []
evidence: []
---

## Outcome

Kuvaa milestoneen kuuluva hyväksytyn tuotteen tai järjestelmän lopputila. Kirjoita mitä pitää olla totta, ei tehtävälistaa.

## Linked Goals

- `goal-000`: [miksi tämä goal kuuluu milestoneen]

## Linked ADRs

- `adr-000`: [mikä päätös rajaa milestonea]

## Exit Gate

Milestone on valmis, kun [konkreettinen hyväksymisehto, testipinta tai julkaisuportti] täyttyy.

Pysähdy, jos [päätös, hyväksyntä, evidence tai raja] puuttuu ja milestone vaatisi sen lukitsemista.

## Evidence

- [Komento, testi, demo, dokumentti, loki, Backlog-evidenssi tai muu havainto]

## Non-Goals

- [Asia, jota milestone ei saa laajentaa tai luvata]

## Constraints

- [Säilytettävä Goal, ADR, ympäristöraja, lähderaja, security-raja tai käyttäjälupaus]

## Status

- State: planned
- Owner: human
- Decision authority: human
```
