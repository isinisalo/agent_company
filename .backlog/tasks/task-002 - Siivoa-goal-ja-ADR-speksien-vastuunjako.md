---
id: TASK-002
title: Siivoa goal- ja ADR-speksien vastuunjako
status: Done
assignee: []
created_date: '2026-06-22 19:16'
updated_date: '2026-06-22 19:19'
labels:
  - spec
  - adr
  - goal
dependencies: []
modified_files:
  - specs/goals
  - specs/adr
priority: medium
ordinal: 2000
---

## Description

<!-- SECTION:DESCRIPTION:BEGIN -->
Erotetaan goal-dokumenttien WHAT/WHY-sisältö ADR-dokumenttien pysyvistä HOW- ja päätösrajoista. Goal-speksit jäävät goal-only-muotoon, ja poistettavat oleelliset päätökset säilytetään ADR:issä.
<!-- SECTION:DESCRIPTION:END -->

## Acceptance Criteria
<!-- AC:BEGIN -->
- [x] #1 Goal-dokumenteissa ei ole CONSTRAINTS-, SOURCE INTENT- tai TECHNOLOGY BOUNDARIES -osioita.
- [x] #2 Goal-dokumentit eivät lukitse teknologiaa, provideria, runtimea, infraa, tietokantaa, auth-teknologiaa tai deployment-mallia.
- [x] #3 ADR-dokumentit säilyttävät oleelliset integraatio-, arkkitehtuuri-, autentikointi-, turvallisuus- ja tuotantokäytön päätökset.
- [x] #4 Uudet tai muokatut ADR:t noudattavat Context/Decision/Consequences-rakennetta.
- [x] #5 Suunnitelman rg-tarkistukset on ajettu ja tulokset dokumentoitu.
<!-- AC:END -->

## Implementation Plan

<!-- SECTION:PLAN:BEGIN -->
1. Poista goal-dokumenteista ADR-tasolle kuuluvat CONSTRAINTS-, SOURCE INTENT- ja TECHNOLOGY BOUNDARIES -sisällöt.
2. Neutraloi goalien provider-, teknologia- ja tuotantokäyttöviittaukset hyväksyttyihin lähde-, päätös- ja operointirajoihin.
3. Päivitä ADR-011 kuvaamaan goalien WHAT/WHY- ja ADR:ien HOW/päätösraja.
4. Lisää sovelluslaajuiset turvallisuus- ja tuotantokäytön stop-säännöt ADR-013:een sekä Auth-kontekstin pysyvät turvallisuusrajat ADR-014:ään.
5. Varmista rakenne ja sisältö rg-tarkistuksilla sekä git diff --checkillä.
<!-- SECTION:PLAN:END -->

## Implementation Notes

<!-- SECTION:NOTES:BEGIN -->
Toteutus noudatti tiukkaa goal-only-rajausta. Provider- ja teknologiatermit poistettiin goal-dokumenteista; pysyvät turvallisuus- ja tuotantokäytön päätökset keskitettiin uusiin ADR:iin.
<!-- SECTION:NOTES:END -->

## Final Summary

<!-- SECTION:FINAL_SUMMARY:BEGIN -->
Goal-dokumentit siivottiin goal-only-muotoon poistamalla CONSTRAINTS-, SOURCE INTENT- ja TECHNOLOGY BOUNDARIES -osiot sekä neutraloimalla provider-/teknologiaviittaukset. ADR-011 päivitettiin kuvaamaan goalien ja ADR:ien vastuunjako. Lisättiin ADR-013 sovelluslaajuisille turvallisuus- ja tuotantokäytön stop-säännöille sekä ADR-014 Auth-kontekstin pysyville turvallisuusrajoille.

Validointi: rg-tarkistukset varmistivat, ettei specs/goals sisällä poistettuja osioita tai suunnitelmassa listattuja teknologia/provider-duplikaatteja. ADR-rg osoitti oleellisten päätösten säilyvän specs/adr-puolella. git diff --check meni läpi.
<!-- SECTION:FINAL_SUMMARY:END -->

## Definition of Done
<!-- DOD:BEGIN -->
- [x] #1 Acceptance criteria on testattu tehtävän scopea vasten
- [x] #2 Relevantit lint typecheck build ja testikomennot on ajettu tai rajaus on kirjattu
- [x] #3 Salaisuuksia tokeneita credentialeja ja PII-tietoja ei palauteta lokiteta tai commitoida
- [x] #4 Julkiset API data infra ja operointisopimukset on päivitetty tarvittaessa
- [x] #5 Final Summary kuvaa toteutuksen tuloksen validoinnin ja rajaukset
<!-- DOD:END -->
