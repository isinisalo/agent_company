---
id: adr-011
title: Valitaan päätöshierarkia ja agentin päätösvalta
date: '2026-06-07'
status: accepted
---
## Context
Projekti tarvitsee yksiselitteisen tavan ratkaista ristiriidat tavoitteen, ADR:ien, Backlog-tehtävien, specien ja toteutuksen välillä.

## Decision
Päätöslähteiden järjestys on: käyttäjän nykyinen vaatimus, goal-dokumentit, hyväksytyt ADR:t, Backlog-tehtävä, relevantit specit ja olemassa oleva toteutus.

Agentti saa päättää HOW-tason yksityiskohdat hyväksyttyjen rajojen sisällä. Projektin tavoitteen, pysyvän arkkitehtuuri-, riski-, kustannus- tai teknologiarajan muutos vaatii käyttäjän hyväksynnän ja tarvittaessa uuden ADR:n.

Goal-dokumentit määrittävät WHAT- ja WHY-tason tavoitteen, käyttäjälle näkyvän lopputilan, product scopen ja onnistumisen evidenssin. ADR-dokumentit määrittävät pysyvät HOW-tason päätökset, teknologiavalinnat, arkkitehtuurirajat, turvallisuusrajat, integraatiorajat ja tuotantokäytön stop-säännöt.

## Consequences

- Alempi päätöslähde ei saa kumota ylempää; ristiriita pysäyttää työn.
- ADR:t määrittävät projektin pysyvät rajat. Goal-dokumentit määrittävät tavoitteen.
- Specit, planit, notesit ja final summaryt dokumentoivat HOW-tason toteutusta tehtävän rajassa.
