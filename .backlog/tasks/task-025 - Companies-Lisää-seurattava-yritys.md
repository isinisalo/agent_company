---
id: TASK-025
title: 'Companies: Lisää seurattava yritys'
status: To Do
assignee: []
created_date: '2026-06-07 11:25'
labels:
  - Companies
  - Backend
milestone: m-5
dependencies:
  - TASK-017
references:
  - .backlog/tasks/task-017 - Detail-spec-Companies-and-watchlist-contract.md
documentation:
  - .backlog/docs/intent/doc-001 - goal.md
  - .backlog/docs/specs/doc-006 - bounded-context-map-and-glossary.md
priority: medium
ordinal: 1000
---

## Description

<!-- SECTION:DESCRIPTION:BEGIN -->
### MITÄ
Toteuta Companies and watchlist -kontekstin käyttötapaus, jossa ylläpitäjä lisää seurattavan suomalaisen yrityksen.

- Yritys lisätään vain detail-specissä hyväksytyllä tunnisteella ja perusdatalla.
- Uusi seurattava yritys saa keruuasetukset hyväksytyn oletuksen mukaan.
- Duplikaattiyritys hylätään tai käsitellään idempotentisti detail-specin mukaan.

### MIKSI
Seurattavat yritykset määrittävät, mitä dataa järjestelmä kerää ja näyttää.
<!-- SECTION:DESCRIPTION:END -->

## Acceptance Criteria
<!-- AC:BEGIN -->
- [ ] #1 GIVEN ylläpitäjä antaa validin yritystunnisteen ja vaaditut tiedot, WHEN yritys lisätään, THEN yritys näkyy seurattavana yrityksenä.
- [ ] #2 GIVEN yritys on jo seurannassa, WHEN sitä lisätään uudelleen, THEN uutta duplikaattia ei synny.
- [ ] #3 GIVEN syöte on puutteellinen tai virheellinen, WHEN lisäystä käsitellään, THEN yritystä ei luoda.
- [ ] #4 GIVEN kutsuja ei ole hallintakäyttäjä, WHEN yritystä yritetään lisätä, THEN toiminto hylätään ennen muutosta.
- [ ] #5 GIVEN yritys lisätään tai hylätään, WHEN vastaus ja lokit muodostetaan, THEN salaisuuksia, credentialeja tai lähteen raw-dataa ei palauteta eikä lokiteta.
<!-- AC:END -->

## Definition of Done
<!-- DOD:BEGIN -->
- [ ] #1 Acceptance criteria on testattu tehtävän scopea vasten
- [ ] #2 Relevantit lint typecheck build ja testikomennot on ajettu tai rajaus on kirjattu
- [ ] #3 Salaisuuksia tokeneita credentialeja ja PII-tietoja ei palauteta lokiteta tai commitoida
- [ ] #4 Julkiset API data infra ja operointisopimukset on päivitetty tarvittaessa
- [ ] #5 Final Summary kuvaa toteutuksen tuloksen validoinnin ja rajaukset
<!-- DOD:END -->
