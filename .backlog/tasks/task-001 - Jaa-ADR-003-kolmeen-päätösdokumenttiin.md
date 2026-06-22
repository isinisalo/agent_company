---
id: TASK-001
title: Jaa ADR-003 kolmeen päätösdokumenttiin
status: Done
assignee:
  - Codex
created_date: '2026-06-22 19:07'
updated_date: '2026-06-22 19:09'
labels: []
dependencies: []
documentation:
  - 'specs/adr/adr-003-[Project]-Valitaan-monorepo.md'
  - 'specs/adr/adr-004-[Project]-Valitaan-GitHub-Actions-CI-CD-putkeksi.md'
  - 'specs/adr/adr-005-[Project]-Valitaan-Mockoon-paikallisiin-REST-mockeihin.md'
modified_files:
  - 'specs/adr/adr-003-[Project]-Valitaan-monorepo.md'
  - 'specs/adr/adr-004-[Project]-Valitaan-GitHub-Actions-CI-CD-putkeksi.md'
  - 'specs/adr/adr-005-[Project]-Valitaan-Mockoon-paikallisiin-REST-mockeihin.md'
  - 'specs/adr/adr-006-[Frontend]-Valitaan-React-Vite-Tailwind-ja-shadcn-ui.md'
  - 'specs/adr/adr-007-[Frontend]-Valitaan-frontend-laadunvarmistus-ja-testit.md'
  - 'specs/adr/adr-008-[Backend]-Valitaan-backend-arkkitehtuurimalli.md'
  - 'specs/adr/adr-009-[Backend]-Valitaan-backend-runtime-ja-kirjastopino.md'
  - 'specs/adr/adr-010-[Backend]-Valitaan-JWT-pohjainen-API-autentikointi.md'
  - >-
    specs/adr/adr-011-[Project]-Valitaan-paatoshierarkia-ja-agentin-paatosvalta.md
  - 'specs/adr/adr-012-[Data]-Valitaan-ulkoisten-palveluiden-integraatiorajat.md'
priority: medium
ordinal: 1000
---

## Description

<!-- SECTION:DESCRIPTION:BEGIN -->
Jaa nykyinen yhdistelmä-ADR kolmeen hyväksyttyyn päätökseen: monorepo, GitHub Actions CI/CD ja Mockoon. Numeroi nykyiset ADR-004...ADR-010 kaksi numeroa eteenpäin ja päivitä tiedostojen frontmatter-id:t vastaamaan uusia nimiä.
<!-- SECTION:DESCRIPTION:END -->

## Acceptance Criteria
<!-- AC:BEGIN -->
- [x] #1 specs/adr sisältää ADR:t adr-001...adr-012 ilman numeroaukkoja tai duplikaatteja.
- [x] #2 ADR-003 käsittelee vain monorepo-päätöstä.
- [x] #3 ADR-004 käsittelee vain GitHub Actions CI/CD -päätöstä.
- [x] #4 ADR-005 käsittelee vain Mockoonin paikallista REST-mock-käyttöä.
- [x] #5 Nykyisten ADR-004...ADR-010 dokumenttien sisältö, status ja päivämäärä säilyvät muuten, mutta tiedostonimi ja frontmatter-id päivittyvät uusiin numeroihin.
- [x] #6 Jokaisen ADR-tiedoston frontmatter-id vastaa tiedoston numeroa.
- [x] #7 ADR-ID-viittaukset tarkistetaan rg-haulla ja päivitetään tarvittaessa.
<!-- AC:END -->

## Implementation Plan

<!-- SECTION:PLAN:BEGIN -->
1. Korvaa yhdistelmä-ADR-003 monorepoa koskevalla ADR:llä.
2. Luo uudet ADR-004 ja ADR-005 GitHub Actions CI/CD- ja Mockoon-päätöksille.
3. Siirrä nykyiset ADR-004...ADR-010 kaksi numeroa eteenpäin ja päivitä frontmatter-id:t.
4. Etsi ADR-ID-viittaukset koko reposta ja päivitä vain tarvittavat sisäiset viittaukset.
5. Validoi tiedostolista, numerointi ja frontmatter-id:t shell-tarkistuksilla.
<!-- SECTION:PLAN:END -->

## Implementation Notes

<!-- SECTION:NOTES:BEGIN -->
Toteutus jakoi yhdistelmä-ADR-003:n kolmeen hyväksyttyyn ADR:ään ja siirsi vanhat ADR-004...ADR-010 kaksi numeroa eteenpäin. Validointi: ADR-sekvenssi 001...012 tarkistettu, frontmatter-id:t tarkistettu, vanhan yhdistelmäotsikon ja tiedostonimen viittaukset tarkistettu rg-haulla.
<!-- SECTION:NOTES:END -->

## Final Summary

<!-- SECTION:FINAL_SUMMARY:BEGIN -->
Jaettu ADR-003 kolmeen erilliseen hyväksyttyyn päätösdokumenttiin: monorepo, GitHub Actions CI/CD ja Mockoon paikallisiin REST-mockeihin. Nykyiset ADR-004...ADR-010 siirrettiin numeroihin ADR-006...ADR-012 ja niiden frontmatter-id:t päivitettiin vastaamaan uusia tiedostonimiä.

Validointi: tarkistettu, että specs/adr sisältää ADR:t 001...012 ilman aukkoja; tarkistettu, että jokaisen tiedoston frontmatter-id vastaa tiedoston numeroa; ajettu rg-haku vanhalle yhdistelmäotsikolle, vanhalle tiedostonimelle ja ADR-ID-viittauksille. Muutos on dokumentaatiomuutos, joten lint/build/test-komentoja ei ajettu.
<!-- SECTION:FINAL_SUMMARY:END -->

## Definition of Done
<!-- DOD:BEGIN -->
- [x] #1 Acceptance criteria on testattu tehtävän scopea vasten
- [x] #2 Relevantit lint typecheck build ja testikomennot on ajettu tai rajaus on kirjattu
- [x] #3 Salaisuuksia tokeneita credentialeja ja PII-tietoja ei palauteta lokiteta tai commitoida
- [x] #4 Julkiset API data infra ja operointisopimukset on päivitetty tarvittaessa
- [x] #5 Final Summary kuvaa toteutuksen tuloksen validoinnin ja rajaukset
<!-- DOD:END -->
