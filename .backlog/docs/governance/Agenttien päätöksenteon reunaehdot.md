---
id: doc-004
title: Agenttien päätöksenteon reunaehdot
type: specification
created_date: '2026-06-07 06:33'
updated_date: '2026-06-07 11:20'
tags:
  - governance
  - aws
  - agents
  - constraints
---
# Agenttien päätöksenteon reunaehdot

## Tarkoitus

Tämä dokumentti määrittää, mitä agentti saa päättää itse ja milloin työ pitää pysäyttää käyttäjän päätöstä varten. Käytä tätä yhdessä `goal.md`:n, bounded context -kartan ja Backlog-tehtävän kanssa.

## Artifact taxonomy

- `goal.md`: käyttäjän määrittämä GOAL, INTENT, WHY, WHAT, rajaukset ja korkean tason teknologiarajat.
- ADR `.backlog/decisions/`: vain käyttäjän hyväksymä korkean tason päätös, joka muuttaa projektin pysyvää arkkitehtuuri-, riski-, kustannus- tai teknologiarajaa.
- Spec `.backlog/docs/specs/`: agentin tuottama HOW-tason toteutussopimus hyväksyttyjen rajojen sisällä.
- Milestone: toimitettava kokonaisuus tai bounded context.
- Task: itsenäinen WHAT/WHY-työmääräys, jossa on acceptance criteria ja validointivaatimus.
- Implementation plan/notes/final summary: tehtäväkohtainen toteutusjälki.

Resetin jälkeen `.backlog/decisions` ei sisällä hyväksyttyjä ADR:iä. Älä kohtele vanhoja päätöstiedostoja lähteenä. Älä luo uutta ADR:ää ilman käyttäjän eksplisiittistä hyväksyntää.

## Päätöshierarkia

Ratkaise epäselvyydet tässä järjestyksessä:

1. Käyttäjän eksplisiittinen vaatimus nykyisessä tehtävässä.
2. `.backlog/docs/intent/goal.md`.
3. Hyväksytyt ADR:t, jos sellaisia on olemassa.
4. Relevantti Backlog-tehtävä ja sen acceptance criteria.
5. Relevantit spec-dokumentit.
6. Olemassa oleva koodi, testit ja paikalliset konventiot.
7. Tämä governance-dokumentti.

Alempi taso ei saa kumota ylempää tasoa. Jos lähteet ovat ristiriidassa, pysähdy ja kirjaa ristiriita tehtävään.

## Agentin päätösvalta

Agentti saa määrittää HOW-tason yksityiskohdat, kun kaikki ehdot täyttyvät:

- päätös pysyy `goal.md`:n rajauksissa
- päätös ei lisää uutta top-level sovellusaluetta, runtimea, frameworkia, AWS-palvelua, autentikointimallia, tietokantaa tai tuotantodatalähdettä
- päätös ei muuta julkista sopimusta ilman siihen kohdistuvaa tehtävää tai spec-tehtävää
- päätös on toteutettavissa ja testattavissa ilman tuotantodataa, oikeita credentialeja tai tuotantodeployta
- päätös voidaan dokumentoida tehtävän plan/notes/final summaryyn tai detail-speciin

Agentti saa kirjoittaa detail-specin, API-sopimuksen, datamallin, infrastruktuurirakenteen tai testistrategian vain sitä koskevan Backlog-tehtävän scopeen.

## Stop rules

Pysähdy ja pyydä käyttäjän päätös tai merkitse tehtävä `Blocked`, jos muutos:

- muuttaisi projektin tavoitetta, OUT OF SCOPE -rajausta tai korkean tason teknologiarajaa
- vaatisi uuden ADR:n mutta ADR:ää ei ole hyväksytty
- lisäisi uuden AWS-palvelun, runtime-version, frameworkin, tietokannan, autentikointimallin, tuotantodatalähteen tai top-level sovellusalueen
- vaatisi tuotantodeployn, tuotantodatan, oikeat credentialit, cloud-oikeudet tai ulkoisen palvelun hyväksymättömät ehdot
- voisi paljastaa salaisuuksia, credentialeja, tokeneita, password hasheja, token-digestejä, API-avaimia, PII:tä tai ulkoisten palvelujen raw credentialeja
- vaatisi liiketoimintasäännön, retention-säännön, legal/compliance-tulkinnan, sijoitusneuvonnan rajan tai cross-context deletion -politiikan arvaamista
- rikkoisi bounded context -omistajuuden tai loisi jaetun domain-paketin ilman hyväksyntää

## Default rules

Kun detail-spec puuttuu, tee pienin palautettava ratkaisu tai luo ensin detail-spec-tehtävä. Älä lukitse pysyvää julkista API:a, DynamoDB-avainmallia, IAM-laajuutta tai deploy-mallia käyttötapaustaskin sivuvaikutuksena.

Domain- ja use case -kerros pysyy riippumattomana HTTP:stä, AWS:stä, DynamoDB:stä, Pydanticista, PynamoDB:stä, boto3:sta, PyJWT:stä, requestsista ja ulkoisten API:en raakamalleista.

Konfiguraatio kuuluu ei-salaisena Parameter Storeen tai paikalliseen vastaavaan konfiguraatiorakenteeseen. Salaisuudet kuuluvat Secrets Manageriin tai testien dummy-arvoihin. Jos luokka on epäselvä, käsittele arvoa salaisuutena ja pysähdy ennen tuotantokäyttöä.

Ulkoiset lähteet ovat mock-only, kunnes niiden käyttöehdot, lisenssi, robots-käytäntö, lähdemaininta, kutsurajat, retention ja credential-käsittely on dokumentoitu ja hyväksytty.

## Validation

Jokaisen taskin final summaryyn kirjataan:

- mitä toteutettiin tai päätettiin
- mitä acceptance criteria -kohtia vasten työ validoitiin
- mitkä komennot ajettiin tai miksi niitä ei voi vielä ajaa
- mitä rajauksia, puutteita tai jatkotehtäviä jäi

Jos `backend/`, `frontend/` tai `infra/` ei vielä sisällä konfiguroituja tarkistuskomentoja, älä keksi uutta toolchainia. Kirjaa puuttuva komento rajoituksena tai luo sitä koskeva tehtävä.
