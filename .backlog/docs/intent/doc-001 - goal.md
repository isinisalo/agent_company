---
id: doc-001
title: Projektin tavoite
type: other
created_date: '2026-06-06 07:19'
updated_date: '2026-06-07 11:19'
tags:
  - intent
  - goal
---
# Projektin tavoite

## GOAL

Rakenna palvelu, jossa suomalaisiin yrityksiin liittyvä seuranta-, markkina-, perustieto- ja keskusteluaineisto näkyy keskitetysti yhdessä selainkäyttöliittymässä.

Palvelun ydin on seurattavien yritysten lista. Järjestelmä kerää, tallentaa ja näyttää yrityksiin liittyvää tietoa niin, että käyttäjän ei tarvitse hakea samaa tietoa käsin erillisistä lähteistä.

## INTENT

Käyttäjä määrittää projektin tavoitteen, rajaukset, hyväksytyt teknologiset päälinjat ja prioriteetin. Agentit määrittävät toteutuksen HOW-tason yksityiskohdat Backlog-tehtävissä ja detail-spesifikaatioissa näiden rajojen sisällä.

Yksityiskohtainen domain-, API-, data-, infra-, operointi- tai testausratkaisu ei kuulu tähän dokumenttiin. Jos agentti tarvitsee detail-ratkaisun, se toteuttaa tai päivittää sitä koskevan tehtävän `Agent detail specifications` -milestonessa.

## WHY

Palvelun tarkoitus on tehdä yritystiedon seurannasta toistettavaa, jäljitettävää ja automatisoitavaa. Rekisteröitynyt käyttäjä voi tarkastella kerättyä tietoa roolinsa sallimissa rajoissa. Ylläpitäjä voi hallita seurattavia yrityksiä ja sitä, mitä tietoa niistä kerätään.

## WHAT

Järjestelmän tulee sisältää nämä bounded contextit:

- `Auth`: käyttäjän rekisteröinti, kirjautuminen, sähköpostivahvistus, salasanan resetointi ja käyttäjähallinta.
- `Notifications`: käyttäjälle lähetettävät viestit, toimituspyynnöt ja toimituksen tila.
- `Companies and watchlist`: seurattavat yritykset, yritysten perustietojen hallinta ja keruuasetukset.
- `Marketdata`: seurattavien yritysten markkinadatan haku, tallennus ja näyttäminen.
- `Comments`: yrityksiin liittyvän keskusteluaineiston haku, tallennus ja näyttäminen.
- `Scheduling`: ajastetut tausta-ajot, keruiden käynnistys ja ajon tilan seuranta.

Hyväksytyt korkean tason teknologiarajat ovat:

- Monorepon sallitut top-level sovellusalueet ovat `backend/`, `frontend/` ja `infra/`.
- Backend on Python 3.14 FastAPI Lambda -backend, joka noudattaa ports and adapters -arkkitehtuuria.
- Frontend on React TypeScript Vite SPA, joka käyttää Tailwind CSS:ää ja shadcn/ui:ta.
- Infra toteutetaan AWS serverless -mallilla ja AWS SAMilla.
- Pysyvä sovellusdata tallennetaan DynamoDB:hen.
- API-autentikointi käyttää JWT bearer -mallia.
- Paikalliset ulkoisten REST API:en mockit toteutetaan Mockoonilla.
- CI/CD toteutetaan GitHub Actionsilla.
- Ulkoiset lähteet ovat EODHD, PRH:n YTJ Open Data API v3 ja Inderes Forum, kun niiden käyttöehdot ja tuotantokäytön rajat on hyväksytty.

## OUT OF SCOPE

Järjestelmä ei tuota sijoitusneuvontaa, osto- tai myyntisuosituksia, automaattisia kaupankäyntipäätöksiä eikä kaupankäyntitoiminnallisuutta.

Järjestelmä ei ole yleinen CRM-, taloushallinto-, analytiikka- tai yritysrekisterijärjestelmä. Yritystiedot mallinnetaan vain seurannan, keruun ja näyttämisen tarpeisiin.

Keskustelukeruu ei ole yleinen sosiaalisen median keräin. Alkuvaiheen keskustelulähde on Inderes Forum vain hyväksytyn compliance-rajauksen jälkeen.

Reaaliaikainen streaming-markkinadata ei kuulu alkuvaiheen tavoitteeseen.

## HIGH-LEVEL CONSTRAINTS

Domain ei saa riippua AWS:n, HTTP:n, DynamoDB:n, FastAPI:n, Pydanticin, JWT-kirjaston tai ulkoisten API:en raakamalleista.

Salaisuuksia, credentialeja, tokeneita, password hasheja, token-digestejä, API-avaimia tai PII:tä ei saa palauttaa API-vastauksissa, julkaista eventeissä, tallentaa fixtureihin tai lokittaa.

Tuotantodeploy, tuotantodata, oikeat credentialit, cloud-oikeudet ja ulkoisten lähteiden tuotantokäyttö vaativat erillisen hyväksytyn tehtävän ja dokumentoidun evidenssin.

Hyväksytyt korkean tason ADR:t ovat `.backlog/decisions/decision-001` - `.backlog/decisions/decision-008`. Detail-tason Auth-päätökset 009-011 eivät ole kanonisia ja niiden sisältö kuuluu agenttien detail-spec-tehtäviin.
