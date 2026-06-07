---
id: doc-005
title: project-structure-and-quality-gates
type: specification
created_date: '2026-06-07 10:52'
updated_date: '2026-06-07 10:52'
tags:
  - specs
  - project
  - quality
  - agents
---
# Project structure and quality gates

## Tarkoitus

Tämä speksi määrittää repo-rakenteen ja laatugatet agenteille. Käytä tätä yhdessä `goal.md`:n, hyväksyttyjen ADR:ien ja agenttien päätöksenteon reunaehtojen kanssa.

## Repo-rakenne

Sallitut top-level sovellusalueet ovat `backend/`, `frontend/` ja `infra/`.

- `backend/` sisältää Python 3.14 FastAPI Lambda -backendin, domainin, use caset, portit, adapterit, composition rootit ja backend-testit.
- `frontend/` sisältää React TypeScript Vite SPA:n, UI-komponentit, frontend-logiikan ja frontend-testit.
- `infra/` sisältää AWS SAM -templatejen, ympäristökohtaisten SAM-konfiguraatioiden, infrastruktuuritestien ja Mockoon-konfiguraatioiden lähteet.
- `.backlog/` sisältää Backlog.md taskit, dokumentit, milestone:t ja ADR:t. Muuta näitä MCP:n tai Backlog CLI:n kautta.
- `.github/` saa sisältää CI/CD-workflowt ja GitHub-metadataa.
- `.agents/` saa sisältää projektikohtaisia agenttitaitoja ja agenttiohjeita.

Älä lisää uutta top-level sovellushakemistoa, jaettua cross-area-pakettia tai deployment-mallia ilman hyväksyttyä ADR:ää. Jos tehtävä tarvitsee yhteistä koodia usean alueen välillä, pysähdy ja pyydä arkkitehtuuripäätös.

## Backend quality gates

Backend-koodi ei saa riippua AWS:stä, HTTP:stä, Pydanticista, PynamoDB:stä, boto3:sta, PyJWT:stä tai requests-kirjastosta domain- tai use case -kerroksessa.

Kun `backend/` on olemassa, vähimmäisvalidointi on:

- domain- ja use case -testit ilman AWS- tai HTTP-riippuvuutta
- adapteritestit moto- tai rajatuilla mockeilla kun AWS-adapteria muutetaan
- responses-pohjaiset testit kun requests-pohjaista ulkoista HTTP-adapteria muutetaan
- `ruff check` ja `ruff format --check` backendin konfiguroidulla komennolla
- `mypy` backendin konfiguroidulla komennolla

Jos backendin test runneria tai komentoa ei ole vielä määritetty repositoryssä, agentti ei saa lisätä uutta testikirjastoa oletuksella. Kirjaa puuttuva komento `Blocked`- tai `Implementation Notes` -merkinnäksi ja tee erillinen päätös tai toteutustehtävä.

## Frontend quality gates

Frontend-koodi käyttää React TypeScriptiä, Viteä, Tailwind CSS:ää ja shadcn/ui:ta. UI käyttää semanttisia teematokeneita raakavärien sijaan.

Kun `frontend/` on olemassa, vähimmäisvalidointi on:

- ESLint frontendin konfiguroidulla komennolla
- Jest yksikkötesteille ja pienille komponenttitesteille
- Playwright käyttäjälle näkyville korkean arvon virroille
- Playwright-testit Given/When/Then-rakenteella
- Page Objectit polussa `frontend/tests/e2e/pages/`

Älä lisää Next.js:ää, SSR:ää, uutta UI-kirjastoa tai uutta tilanhallintakirjastoa ilman hyväksyttyä ADR:ää.

## Infra quality gates

Infrastruktuurin lähde on `infra/`-hakemiston AWS SAM -template ja siihen liittyvät ympäristökohtaiset konfiguraatiot.

Kun `infra/` on olemassa, vähimmäisvalidointi on:

- SAM-template validoitu konfiguroidulla komennolla
- IAM-politiikat tarkistettu least privilege -periaatetta vasten
- CORS-originien, Parameter Store -polkujen ja Secrets Manager -nimien ympäristöerottelu tarkistettu
- deploy-komennot ajettu vain hyväksyttyyn ympäristöön ja vain tehtävän deploy-scopen sisällä

Tuotantoresurssien luonti, poisto, migraatio tai deploy vaatii eksplisiittisen deploy-scopen.

## CI-gatet

Pull requestin tulee ajaa touched-area-periaatteella vähintään ne tarkistukset, jotka vastaavat muutettuja hakemistoja. Jos sovellusalueen komennot puuttuvat, PR ei saa väittää täyttä validointia läpäistyksi.

CI ei saa käyttää pitkäikäisiä AWS access key -avaimia. AWS-julkaisut käyttävät ensisijaisesti GitHub Actions OIDC -luottamusta.

## Acceptance

- Agentti osaa nimetä sallitut top-level sovellushakemistot.
- Agentti pysähtyy ennen uuden top-level sovellusalueen tai frameworkin lisäämistä.
- Agentti raportoi puuttuvan validointikomennon eikä keksi uutta toolchainia ilman päätöstä.
- Agentti kirjaa toteutuksen validointievidenssin Backlog root taskiin.
