---
id: goal-004
title: Projektin ohjaus
type: other
created_date: '2026-06-07 12:34'
updated_date: '2026-06-23'
status: accepted
owner: human
version: 1
supersedes: []
decision_authority: human
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
- Taskikohtaisen aktiivisen Codex `/goal`-työtilan muodostaminen hyväksytyistä Goaleista, ADR:istä ja Backlog-tehtävästä ilman, että `/goal` korvaa pysyviä Goal- tai ADR-dokumentteja.

## ACTIVE CODEX GOAL MODEL

Jokaiselle agenttiajolle tulee muodostaa aktiivinen `/goal`, kun työ perustuu hyväksyttyyn Backlog-tehtävään tai toteuttaa hyväksyttyä Goal-dokumenttia. Aktiivinen `/goal` on säikeeseen persistoitu työtila. Se ei ole projektitason Goal, ADR, milestone, task eikä päätöslähde.

Aktiivisen `/goal`-tekstin tulee sisältää nämä osat tässä järjestyksessä:

- Outcome: määritä hyväksytystä Goalista ja tehtävästä toteutettava konkreettinen lopputulos.
- Verification surface: nimeä testit, näkyvä käyttäytyminen, tiedostot, komennot ja Backlog-evidenssi, joilla lopputulos todennetaan.
- Constraints: listaa säilytettävät ADR:t, tuotteen käyttäjälupaus, lähderajat, security-rajat ja muut ei-neuvoteltavat ehdot.
- Boundaries: nimeä sallitut muutosalueet, ympäristörajat ja kielletyt ympäristöt kuten tuotanto ilman eksplisiittistä hyväksyntää.
- Iteration policy: jokaisen epäonnistuneen yrityksen jälkeen kirjaa evidenssi ja valitse olennaisesti erilainen, palautettava toteutustapa hyväksytyn Goalin ja ADR:ien sisällä.
- Blocked stop condition: pysähdy, kun hyväksytyn Goalin, ADR:ien ja tehtävän sisällä ei ole jäljellä validia toteutuspolkua. Raportoi kokeillut polut ja täsmällinen ihmispäätös tai puuttuva syöte, jota eteneminen vaatii.

Aktiivinen `/goal` ei saa laajentaa hyväksyttyä tuotetavoitetta, lisätä uutta ulkoista tietolähdettä, muuttaa käyttäjälle näkyvää lupausta, ohittaa ADR:ää eikä tehdä tuotantotoimia ilman eksplisiittistä hyväksyntää.

## EVIDENCE

Tavoite täyttyy, kun agentti pystyy lukemaan tavoitteet, ADR:t ja tarkentavat speksit ja päättelemään mitä saa muuttaa, mitä pitää säilyttää, miten aktiivinen taskikohtainen `/goal` muodostetaan ja missä kohdassa työ pitää pysäyttää käyttäjän tai projektin päätöstä varten.
