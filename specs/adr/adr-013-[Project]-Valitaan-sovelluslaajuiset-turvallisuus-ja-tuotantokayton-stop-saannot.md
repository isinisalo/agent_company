---
id: adr-013
title: Valitaan sovelluslaajuiset turvallisuus- ja tuotantokäytön stop-säännöt
date: '2026-06-22'
status: accepted
---
## Context
Projekti tarvitsee yhden pysyvän päätöspinnan sovelluslaajuisille turvallisuus-, lokitus-, dokumentointi- ja tuotantokäytön stop-säännöille, jotta goal-dokumentit voivat kuvata tavoitetta ilman päätösrajaduplikaatteja.

## Decision
Salaisuuksia, tokeneita, credentialeja, salasanoja, token-digestejä, password hasheja, API-avaimia, JWT:itä, PII:tä, tokenillisia URL:eja, cookie-/session-arvoja tai providerin raw-salaisuuksia ei saa palauttaa API-vastauksissa, julkaista tapahtumissa, tallentaa fixtureihin tai testidataan, dokumentoida, commitoida tai lokittaa.

Tuotantodeploy, tuotantodata, cloud-oikeudet, tuotantocredentialit, ulkoisten palveluiden tuotantokutsut, oikeat viestipalveluntarjoajat ja tuotantolähetykset vaativat eksplisiittisen hyväksynnän ja dokumentoidun evidenssin ennen toteutusta tai käyttöä.

Tuotantokäytön hyväksyntä vaatii vähintään käyttöehdot, credential-käsittelyn, kutsurajat, aikakatkaisut, retry-rajat, retentionin, virheluokat, lokitusrajat, IAM- tai muun käyttöoikeusrajan ja operointimallin.

## Consequences

- Agentin tulee estää tuotantokäyttö, tuotantokutsu tai tuotantolähetys, jos vaadittu hyväksyntä tai evidenssi puuttuu.
- Agentin tulee merkitä puuttuva tuotanto-, turvallisuus- tai compliance-raja blocked-tilaan tai pyytää käyttäjän päätös ennen pysyvää muutosta.
- Dokumentit, testidata, fixturet, lokit ja lähdekoodi eivät saa sisältää salaisia arvoja tai tokenillisia reference-URL:eja.
- Raw-provider-virheet normalisoidaan turvalliseksi virheluokaksi ennen lokitusta, API-vastausta tai pysyvää tallennusta.
- Uusi cloud-oikeus, laaja wildcard-oikeus, uusi tuotantopalvelu tai pysyvä konsolimuutos vaatii hyväksytyn päätöspinnan ennen käyttöä.
