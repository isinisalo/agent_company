---
id: decision-003
title: Valitaan monorepo, GitHub Actions ja Mockoon
date: '2026-06-06'
status: accepted
---
## Context
Projekti tarvitsee selkeän hakemistorakenteen automaattisille agenteille, versionhallintaan kytketyn CI/CD-putken ja tavan mockata ulkoisia REST API -palveluita paikallisessa kehityksessä.

## Decision
Repository toteutetaan monorepona, jonka top-level sovellusalueet ovat `backend/`, `frontend/` ja `infra/`. GitHub Actions valitaan CI/CD-ratkaisuksi ja Mockoon REST API -mockaukseen paikallisessa kehityksessä.

## Consequences

- Sovelluskoodi sijoitetaan vastuualueensa mukaiseen top-level-hakemistoon.
- Uudet top-level sovellushakemistot, jaetut cross-area-paketit, runtime-versiot, frameworkit ja deployment-mallin muutokset vaativat käyttäjän hyväksynnän.
- Pull requestien tulee ajaa vähintään aluekohtaiset testit ja quality gate -tarkistukset.
- Jos alueen tarkistuskomentoa ei ole määritetty, puute kirjataan rajoituksena eikä uutta toolchainia keksitä käyttötapaustaskissa.
- AWS-julkaisut toteutetaan ensisijaisesti OIDC-pohjaisella GitHub Actions -luottamuksella ilman pitkäikäisiä AWS-avaimia.
- Mockoon-konfiguraatiot versionhallitaan, mutta tuotantokoodi ei saa riippua Mockoonista.
- Mockit eivät korvaa sopimusten tai integraatioiden varsinaista validointia.
