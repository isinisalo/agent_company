---
id: goal-001
title: goal
type: other
created_date: '2026-06-06 07:19'
updated_date: '2026-06-07 12:43'
tags:
  - intent
  - goal
---
# Projektin tavoite

## GOAL

Rakenna selainkäyttöinen palvelu, jossa käyttäjä voi seurata suomalaisia yrityksiä ja nähdä samassa näkymässä yrityksen perustiedot, markkinadatan, yritykseen liittyvän keskusteluaineiston ja tiedonkeruun tilan.

Palvelun onnistunut lopputila on, että seurattava yritys lisätään järjestelmään kerran, minkä jälkeen järjestelmä kerää, tallentaa, attribuoi ja näyttää yritykseen liittyvän tiedon ilman, että käyttäjän täytyy hakea sama tieto käsin erillisistä lähteistä.

## INTENT

Agenttien tulee tehdä ratkaisuja kohti keskitettyä yritysseurantapalvelua, ei yleistä CRM:ää, sijoitusneuvontatyökalua, yritysrekisteriä tai sosiaalisen median keräintä.

Toteutuksen tulee priorisoida jäljitettävää tiedonkeruuta, lähdeattribuutiota, turvallista käyttäjähallintaa, mock-only-kehitystä ja tuotantokäytön eksplisiittisiä stop-sääntöjä. HOW-tason ratkaisut saa määrittää vain hyväksyttyjen ADR:ien ja näiden intent-dokumenttien rajojen sisällä.

## PRODUCT SCOPE

Järjestelmän bounded contextit ovat:

- `Auth`: käyttäjän rekisteröinti, kirjautuminen, sähköpostivahvistus, salasanan resetointi ja admin-käyttäjähallinta.
- `Notifications`: viestien toimituspyynnöt, renderöinti, mock-only-toimitus ja toimitustila.
- `Companies and watchlist`: seurattavat yritykset, yritysten perustiedot ja keruuasetukset.
- `Marketdata`: seurattavien yritysten markkinadatan haku, normalisointi, tallennus ja näyttäminen.
- `Comments`: yrityksiin liittyvän keskusteluaineiston topic-perusteinen haku, deduplikointi, tallennus ja näyttäminen.
- `Scheduling`: ajastetut keruuajot, run-state, retryt, tulosten tallennus ja compliance-puutteisen tuotantokeruun esto.

Osa-alueiden tavoite- ja päätösrajat ovat näissä dokumenteissa:

- `.backlog/docs/intent/goal-004 - Project-delivery-and-agent-spec-goals.md`
- `.backlog/docs/intent/goal-005 - Auth-bounded-context-goal.md`
- `.backlog/docs/intent/goal-006 - Notifications-bounded-context-goal.md`
- `.backlog/docs/intent/goal-007 - Companies-and-watchlist-bounded-context-goal.md`
- `.backlog/docs/intent/goal-008 - Marketdata-bounded-context-goal.md`
- `.backlog/docs/intent/goal-009 - Comments-bounded-context-goal.md`
- `.backlog/docs/intent/goal-010 - Scheduling-bounded-context-goal.md`

## SOURCE INTENT

Hyväksytyt ulkoiset lähteet ovat EODHD markkinadataan, PRH:n YTJ Open Data API v3 yritysten perustietoihin ja Inderes Forum keskusteluaineistoon. Yritykseen liittyvä Inderes Forum -kommentointi haetaan yritykselle määritetyn topicin perusteella.

Ulkoisten lähteiden alkuvaiheen käyttö on mock-only. Tuotantokäyttö vaatii hyväksytyt käyttöehdot, credential-käsittelyn, kutsurajat, aikakatkaisut, retentionin, virheluokat, lokirajat ja dokumentoidun evidenssin.

## TECHNOLOGY BOUNDARIES

- Monorepon sallitut top-level sovellusalueet ovat `backend/`, `frontend/` ja `infra/`.
- Backend on Python 3.14 FastAPI Lambda -backend, joka noudattaa ports and adapters -arkkitehtuuria.
- Frontend on React TypeScript Vite SPA, joka käyttää Tailwind CSS:ää ja shadcn/ui:ta.
- Infra toteutetaan AWS serverless -mallilla ja AWS SAMilla.
- Pysyvä sovellusdata tallennetaan DynamoDB:hen.
- API-autentikointi käyttää JWT bearer -mallia.
- Paikalliset ulkoisten REST API:en mockit toteutetaan Mockoonilla.
- Yksikkötesteissä AWS palvelut mockataan moto5 avulla ja ulkoiset kutsut responses kirjastolla.
- CI/CD toteutetaan GitHub Actionsilla.

## CONSTRAINTS

- Domain ei saa riippua AWS:n, HTTP:n, DynamoDB:n, FastAPI:n, Pydanticin, JWT-kirjaston tai ulkoisten API:en raakamalleista.
- Salaisuuksia, credentialeja, tokeneita, password hasheja, token-digestejä, API-avaimia, JWT:itä tai PII:tä ei saa palauttaa API-vastauksissa, julkaista eventeissä, tallentaa fixtureihin tai lokittaa.
- Tokenillisia reference-URL:eja tai credentialeja ei saa tallentaa dokumentteihin.
- Tuotantodeploy, tuotantodata, oikeat credentialit, cloud-oikeudet ja ulkoisten lähteiden tuotantokäyttö vaativat erillisen hyväksynnän ja dokumentoidun evidenssin.
- Järjestelmä ei tuota sijoitusneuvontaa, osto- tai myyntisuosituksia, automaattisia kaupankäyntipäätöksiä eikä kaupankäyntitoiminnallisuutta.
- Reaaliaikainen streaming-markkinadata ei kuulu alkuvaiheen tavoitteeseen.

## EVIDENCE

Tavoite etenee oikeaan suuntaan, kun agentti pystyy osoittamaan konkreettisilla dokumenteilla, testeillä tai toimivalla koodilla, että seurattavan yrityksen lisääminen, tiedon keruu, lähdeattribuoitu tallennus, selaimessa näkyvä koontinäkymä, käyttäjän autentikointi ja tuotantokeruun stop-säännöt toimivat ilman salaisuuksien vuotoa.
