---
id: doc-008
title: config-secrets-catalog
type: specification
created_date: '2026-06-07 10:53'
updated_date: '2026-06-07 11:21'
tags:
  - specs
  - config
  - secrets
  - aws
---
# Config and secrets catalog

## Tarkoitus

Tämä speksi määrittää konfiguraation ja salaisuuksien luokittelurajat. Se ei ole lopullinen parametrikatalogi. Context-kohtaiset nimet, lukijat ja IAM-oikeudet määritetään detail-spec- tai infra-tehtävissä.

## Storage rules

Ei-salainen ympäristökohtainen konfiguraatio kuuluu Parameter Storeen tai paikalliseen vastaavaan konfiguraatioon.

Salaisuudet ja credential-luonteiset arvot kuuluvat Secrets Manageriin tai testien dummy-arvoihin.

Jos arvo voi olla sekä konfiguraatio että salaisuus, käsittele sitä salaisuutena, kunnes detail-spec tai käyttäjän päätös toisin määrää.

## Naming rules

Nimen tulee kertoa ympäristö, bounded context ja käyttötarkoitus ilman arvon lukemista.

Älä kovakoodaa ympäristöä, tilitunnusta, aluetta, ARNia, tuotantoresurssin nimeä, API-avainta, tokenia tai credentialia sovelluskoodiin.

## Access rules

Lambda, adapteri tai muu runtime-komponentti saa lukea vain oman käyttötapauksensa tarvitsemat arvot.

Laaja lukuoikeus usean contextin parametreihin tai salaisuuksiin vaatii detail-specin ja käyttäjän hyväksynnän, jos vaikutus on pysyvä tai tuotantoon ulottuva.

## Stop rules

Pysähdy, jos uusi salaisuus tarvitsee kierrätysmallin, omistajan tai tuotantoarvon.

Pysähdy, jos tuotantoarvoa tarvitaan paikallisessa testissä.

Pysähdy, jos salaisuuden nimi, sijainti, lukija tai dataluokka on epäselvä.

## Acceptance

Agentti valitsee Parameter Storen ja Secrets Managerin välillä dataluokan perusteella.

Agentti kirjaa uuden parametrin tai salaisuuden käyttötarkoituksen detail-speciin tai taskin final summaryyn.

Agentti ei lisää oikeita arvoja repositoryyn, testifixtureihin, `.env`-esimerkkeihin, lokiin tai virheviesteihin.
