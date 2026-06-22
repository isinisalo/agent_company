---
id: goal-004
title: Projektin ohjaus
type: other
created_date: '2026-06-07 12:34'
updated_date: '2026-06-22'
tags:
  - intent
  - goal
  - project
  - spec
---
# Projektin ohjaus

## GOAL

Varmista, että agentit rakentavat samaa yritysseurantapalvelua samojen tavoitteiden, päätösten ja tarkentavien speksien mukaisesti.

## INTENT

Goal-dokumentit kertovat mitä tuotteen pitää saada aikaan ja miksi. ADR-dokumentit kertovat pitkäikäiset päätökset ja rajat. Tarkentavat speksit ja tehtävät saavat kuvata toteutusta vain hyväksyttyjen tavoitteiden ja päätösten sisällä.

Agentti saa tehdä työn kannalta tarpeellisia pieniä valintoja, kun valinta ei muuta hyväksyttyä tuotetavoitetta, ADR-päätöstä, käyttäjälle näkyvää lupausta tai lähderoolia. Jos työ muuttaisi mitä palvelu lupaa käyttäjälle, mitä tietolähdettä käytetään tai mitä pysyvää rajaa noudatetaan, agentin tulee pysähtyä päätöstä varten.

## CAPABILITIES

- Goalien, ADR:ien ja tarkentavien speksien vastuunjaon säilyttäminen.
- Uuden työn rajaaminen hyväksyttyyn yritysseurannan lopputilaan.
- Ristiriitojen tunnistaminen silloin, kun speksi, tehtävä tai toteutus muuttaisi hyväksyttyä tavoitetta tai päätöstä.
- Päätöstarpeen näkyväksi tekeminen ennen kuin agentti lukitsee uuden pysyvän suunnan.

## EVIDENCE

Tavoite täyttyy, kun agentti pystyy lukemaan tavoitteet, ADR:t ja tarkentavat speksit ja päättelemään mitä saa muuttaa, mitä pitää säilyttää ja missä kohdassa työ pitää pysäyttää käyttäjän tai projektin päätöstä varten.
