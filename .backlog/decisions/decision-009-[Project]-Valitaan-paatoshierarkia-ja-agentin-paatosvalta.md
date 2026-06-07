---
id: decision-009
title: Valitaan päätöshierarkia ja agentin päätösvalta
date: '2026-06-07'
status: accepted
---
## Context
Projekti tarvitsee yksiselitteisen tavan ratkaista ristiriidat tavoitteen, ADR:ien, Backlog-tehtävien, specien ja toteutuksen välillä.

## Decision
Päätöslähteiden järjestys on: käyttäjän nykyinen vaatimus, `docs/intent`, hyväksytyt ADR:t, Backlog-tehtävä, relevantit specit ja olemassa oleva toteutus.

Agentti saa päättää HOW-tason yksityiskohdat hyväksyttyjen rajojen sisällä. Projektin tavoitteen, pysyvän arkkitehtuuri-, riski-, kustannus- tai teknologiarajan muutos vaatii käyttäjän hyväksynnän ja tarvittaessa uuden ADR:n.

## Consequences

- Alempi päätöslähde ei saa kumota ylempää; ristiriita pysäyttää työn.
- ADR:t määrittävät projektin pysyvät rajat. `docs/intent` määrittää tavoitteen.
- Specit, planit, notesit ja final summaryt dokumentoivat HOW-tason toteutusta tehtävän rajassa.
- Detail-tason Auth-päätökset 009-011 eivät kuulu kanoniseen päätösjoukkoon.
