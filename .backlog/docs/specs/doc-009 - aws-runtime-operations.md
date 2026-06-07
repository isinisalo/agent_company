---
id: doc-009
title: aws-runtime-operations
type: specification
created_date: '2026-06-07 10:54'
tags:
  - specs
  - aws
  - operations
  - deploy
---
# AWS runtime operations

## Tarkoitus

Tämä speksi määrittää AWS runtime-, deploy-, rollback-, smoke test-, lokitus- ja hälytysrajat agenteille. Käytä tätä aina, kun muutos koskee `infra/`-hakemistoa, Lambda-ajomallia, API Gatewaytä, CloudFrontia, EventBridgeä, DynamoDB:tä, IAM:ia, Parameter Storea, Secrets Manageria tai deployta.

## Infrastructure source

AWS-infrastruktuurin lähde on versionhallittu AWS SAM -template `infra/`-hakemistossa. Pysyviä konsolimuutoksia ei saa käyttää ratkaisuna.

Ympäristöt ovat `dev`, `test` ja `prod`. Koodi ja template eivät saa kovakoodata tiliä, aluetta, ympäristöä, ARNia, salaisuutta tai tuotantoresurssin nimeä.

Resurssinimien oletusmuoto on:

```text
agent-company-<env>-<context>-<purpose>
```

Parameter Store -polut ja Secrets Manager -nimet määritellään `config-secrets-catalog`-speksissä.

## Deploy rules

Deploy on sallittu vain, kun Backlog root task tai deployment task määrittää ympäristön, komennot, branchin tai commitin, tarvittavat oikeudet ja smoke testin.

Oletusdeploy-komennot ovat käytettävissä vasta, kun `infra/` sisältää SAM-konfiguraation:

```text
sam validate
sam build
sam deploy --config-env <env>
```

Jos SAM-konfiguraatiota, target-ympäristöä tai oikeuksia ei ole, DevOps-agentti kirjaa `Blocked` ja nimeää yhden puuttuvan inputin.

Tuotantodeploy vaatii erillisen hyväksynnän. Agentti ei saa päätellä tuotantodeployta tehtävän yleisestä toteutuspyynnöstä.

## Rollback rules

Jokaisella deployattavalla muutoksella pitää olla rollback-kuvaus ennen test- tai prod-deployta. Vähimmäisrollback on:

- tunnista edellinen toimiva commit tai julkaistu artefakti
- palauta SAM-stack edelliseen templateen ja konfiguraatioon
- peruuta tai sammuta uusi EventBridge-sääntö, jos muutos liittyy ajastukseen
- poista uusi julkinen endpoint tai feature flagaa se pois, jos API-käyttö on riskialtis
- älä tee datamigraation rollbackia ilman erillistä datasuunnitelmaa

DynamoDB-avainten, indeksien tai datan migraation rollback vaatii erillisen päätöksen.

## Smoke tests

Deployn smoke test ei saa käyttää tuotantosalaisuuksia eikä lokittaa käyttäjädataa. Smoke testin pitää tarkistaa vain tehtävän kannalta kriittinen käyttäytyminen.

Vähimmäissmoke test test-ympäristössä:

- API health tai sovittu kevyt endpoint vastaa
- autentikoitu endpoint hylkää puuttuvan tai virheellisen tokenin
- uusi endpoint palauttaa odotetun statuskoodin mock- tai testidatalla
- ajastettu worker voidaan käynnistää testitapahtumalla ilman tuotantokeruuta

## Observability

Lokien tulee olla rakenteisia. Vähimmäiskentät ovat request id tai correlation id, environment, bounded context, use case, result ja error class.

Älä lokita PII:tä, salaisuuksia, API-avaimia, tokeneita, password hasheja, token digestejä, ulkoisten palvelujen raw credential -arvoja tai sisäisiä avainmateriaaleja.

Lisää metriikka tai hälytys, kun muutos koskee:

- kirjautumista tai auth-hylkäyksiä
- Lambda-timeoutteja
- DynamoDB conditional failure -tilanteita
- ulkoisen API:n timeoutteja tai rate limit -virheitä
- EventBridge-tausta-ajojen epäonnistumisia
- DLQ- tai uudelleenajopolkuja

## IAM

IAM toteutetaan least privilege -periaatteella. Jokaisen Lambda-funktion tai pienen funktioryhmän rooli sallii vain tarvittavat actionit rajattuihin resursseihin.

Wildcard on sallittu vain, jos AWS-palvelu ei tue resurssirajausta kyseiselle actionille. Syy dokumentoidaan templateen tai ADR:ään.

CI/CD-rooli, runtime-rooli ja paikalliskehityksen oikeudet pidetään erillään.

## Stop rules

Pysähdy ja pyydä päätös, jos:

- tehtävä vaatii uutta AWS-palvelua
- deploy-target tai oikeudet puuttuvat
- rollbackia ei voi kuvata turvallisesti
- muutos koskee DynamoDB-avaimia, indeksejä tai tuotantodataa
- IAM vaatisi laajaa wildcardia
- tuotantoresurssin luonti, poisto tai migraatio olisi tarpeen

## Acceptance

- Agentti osaa erottaa infra-suunnittelun ja deploy-suorituksen.
- Agentti ei deployaa ilman targettia, oikeuksia, komentoja ja smoke testia.
- Agentti kirjaa deploy-blockerin, jos jokin prerequisite puuttuu.
