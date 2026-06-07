---
id: doc-005
title: project-structure-and-quality-gates
type: specification
created_date: '2026-06-07 10:52'
updated_date: '2026-06-07 11:20'
tags:
  - specs
  - project
  - quality
  - agents
---
# Project structure and quality gates

## Tarkoitus

Tämä speksi määrittää repo-rakenteen ja validoinnin vähimmäisrajat. Se ei päätä sisäisiä pakettinimiä, testikomentoja tai CI-toteutusta ennen kuin niitä koskeva detail-spec tai toteutustehtävä on tehty.

## Repo boundaries

Sallitut top-level sovellusalueet ovat `backend/`, `frontend/` ja `infra/`.

- `backend/` sisältää Python 3.14 FastAPI Lambda -backendin.
- `frontend/` sisältää React TypeScript Vite SPA:n.
- `infra/` sisältää AWS SAM -infrastruktuurin ja paikallisen integraatiotuen.
- `.backlog/` sisältää taskit, milestone:t, dokumentit ja mahdolliset käyttäjän hyväksymät ADR:t.
- `.agents/` sisältää projektikohtaiset agenttiohjeet ja taidot.

Älä lisää uutta top-level sovellushakemistoa, jaettua cross-area-pakettia, runtimea, frameworkia tai deployment-mallia ilman käyttäjän hyväksymää ADR:ää.

## Quality gates

Kun sovellusalue on olemassa, agentti ajaa kapeimmat relevantit tarkistukset kosketetulle alueelle.

Backend-validointi kattaa domain/use case -testit ilman AWS-riippuvuutta, adapteritestit mockeilla, Ruffin ja mypyn, kun komennot on määritetty.

Frontend-validointi kattaa ESLintin, yksikkötestit ja Playwrightin käyttäjälle näkyville korkean arvon virroille, kun komennot on määritetty.

Infra-validointi kattaa SAM-templatejen validoinnin, IAM least privilege -tarkistuksen ja ympäristöerottelun, kun `infra/` on olemassa.

Jos komentoa ei ole määritetty, agentti ei keksi uutta toolchainia käyttötapaustaskissa. Puuttuva komento kirjataan rajoituksena tai sille luodaan detail-/setup-tehtävä.

## Acceptance

Agentti osaa nimetä sallitut top-level sovellusalueet.

Agentti pysähtyy ennen uuden top-level sovellusalueen, runtime-version, frameworkin tai deployment-mallin lisäämistä.

Agentti raportoi ajetut tarkistukset tai puuttuvat komennot taskin final summaryssa.
