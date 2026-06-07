---
id: doc-009
title: aws-runtime-operations
type: specification
created_date: '2026-06-07 10:54'
updated_date: '2026-06-07 11:21'
tags:
  - specs
  - aws
  - operations
  - deploy
---
# AWS runtime operations

## Tarkoitus

Tämä speksi määrittää AWS runtime-, deploy- ja operointirajat. Se ei määritä lopullisia SAM-resursseja, IAM-policyjä, hälytyksiä tai deploy-komentoja ennen detail-spec- tai infra-tehtävää.

## Runtime boundaries

AWS-infrastruktuurin lähde on versionhallittu `infra/`-alue. Pysyviä konsolimuutoksia ei käytetä ratkaisuna.

Julkinen selainkäyttöliittymä julkaistaan CloudFrontin kautta. Julkinen HTTP API kulkee API Gatewayn kautta Lambda-funktioille. Ajastukset ja tausta-ajot toteutetaan hyväksytyn AWS serverless -rajan sisällä.

Lambda-funktiot ovat tilattomia. Pysyvä tila kuuluu hyväksyttyyn tietovarastoon, ei prosessin muistiin, `/tmp`-hakemistoon tai globaaleihin muuttujiin.

## Deploy rules

Deploy on sallittu vain tehtävässä, jossa on eksplisiittinen deploy-scope, target-ympäristö, tarvittavat oikeudet, validointikomennot ja smoke test -raja.

Tuotantodeploy vaatii erillisen hyväksynnän. Agentti ei päättele tuotantodeployta yleisestä toteutuspyynnöstä.

Jos target, oikeudet, komennot tai rollback-raja puuttuvat, merkitse deploy-osuus `Blocked` ja jatka vain turvallisesti paikalliseen toteutukseen.

## Operations rules

Runtime-lokit ja metriikat eivät saa sisältää PII:tä, salaisuuksia, credentialeja, tokeneita, password hasheja, token-digestejä, API-avaimia tai ulkoisen palvelun raw credentialeja.

IAM-oikeudet toteutetaan least privilege -periaatteella. Laaja wildcard vaatii perustelun ja käyttäjän hyväksynnän, jos vaikutus on pysyvä tai tuotantoon ulottuva.

Ulkoisiin API-lähteisiin kohdistuvat kutsut tarvitsevat timeoutin, virherajan ja kutsurajoja kunnioittavan suunnitelman ennen tuotantokäyttöä.

## Stop rules

Pysähdy, jos muutos vaatii uuden AWS-palvelun, tuotantoresurssin luomisen, poistamisen, migraation tai tuotantodeployn.

Pysähdy, jos rollbackia ei voi kuvata turvallisesti.

Pysähdy, jos IAM tarvitsee laajaa wildcardia tai usean contextin oikeuksia.

## Acceptance

Agentti erottaa infrastruktuurin suunnittelun, paikallisen toteutuksen ja deploy-suorituksen.

Agentti ei deployaa ilman targettia, oikeuksia, komentoja, rollback-rajaa ja smoke testia.

Agentti kirjaa operointiriskit ja validointirajat taskin final summaryyn.
