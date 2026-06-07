---
id: goal-004
title: Project delivery and agent spec goals
type: other
created_date: '2026-06-07 12:34'
updated_date: '2026-06-07 12:44'
tags:
  - intent
  - goal
  - project
  - spec
---
# Project delivery and agent spec goals

## GOAL

Mahdollista se, että agentit voivat rakentaa yritysseurantapalvelua johdonmukaisesti hyväksytyn arkkitehtuurin, teknologiarajojen ja turvallisuusrajojen sisällä ilman, että jokainen toteutustehtävä joutuu arvaamaan projektin perusrakenteen.

## INTENT

Tämän dokumentin tehtävä on rajata agenttien päätösvalta. Agentti saa valita HOW-tason toteutuksen silloin, kun valinta ei muuta projektin hyväksyttyjä teknologia-, data-, API-, infra-, autentikointi-, deploy- tai compliance-rajoja.

Kun toteutus lukitsisi julkisen sopimuksen tai pitkäikäisen rakenteen, agentin tulee tehdä valinta eksplisiittisessä detail-spesifikaatiossa tai pysähtyä käyttäjän päätöstä varten.

## REQUIRED SPEC SURFACES

- Repo-rakenne ja laatukomennot: `backend/`, `frontend/` ja `infra/` -alueiden sisäinen rakenne sekä kapeimmat validointikomennot.
- API boundary -konventiot: versiointi, principal, bearer-tokenin raja, virhevastaukset, CORS-vaikutukset ja raw-mallien vuotamattomuus.
- Bounded context -kartta ja sanasto: Auth, Notifications, Companies and watchlist, Marketdata, Comments ja Scheduling erillisinä vastuualueina.
- Context-kohtaiset domain-, API- ja persistence-sopimukset: vain kyseisen osa-alueen toteutukselle tarpeellinen sopimus.
- Operointi- ja compliance-rajat: tuotantodeploy, credentialit, ulkoisten lähteiden tuotantokäyttö, retention, lokitus ja IAM-scope.

## CONSTRAINTS

- Älä luo uutta top-level sovellushakemistoa, runtimea, frameworkia, tietokantaa, pilvipalvelua, autentikointimallia tai deployment-mallia ilman käyttäjän hyväksymää ADR:ää.
- Älä lukitse julkista API:a, DynamoDB key/index -mallia, IAM-scopea, deploy-mallia tai cross-context-sopimusta ilman relevanttia detail-spesifikaatiota.
- Älä lokita, dokumentoi, commitoi tai palauta tokeneita, API-avaimia, credentialeja, salasanoja, token-digestejä, password hasheja, JWT:itä, PII:tä tai tokenillisia URL:eja.
- Jos validointikomentoa ei ole määritetty, kirjaa puute rajoituksena. Älä keksi uutta toolchainia yksittäisen käyttötapauksen yhteydessä.

## EVIDENCE

Tämä tavoite täyttyy, kun agentti pystyy osoittamaan, että uusi toteutus sijoittuu hyväksyttyyn monoreporakenteeseen, käyttää hyväksyttyjä rajapintoja, ajaa tai dokumentoi kapeimmat relevantit tarkistukset, eikä muuta pysyviä sopimuksia ilman hyväksyttyä päätöspintaa.
