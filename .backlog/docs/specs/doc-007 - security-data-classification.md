---
id: doc-007
title: security-data-classification
type: specification
created_date: '2026-06-07 10:53'
tags:
  - specs
  - security
  - data
  - privacy
---
# Security data classification

## Tarkoitus

Tämä speksi määrittää dataluokat, lokitusrajat, säilytys- ja poistoperiaatteet sekä agenttien pysähtymissäännöt. Käytä tätä kaikkien Auth-, API-, integraatio-, lokitus- ja tietomallimuutosten yhteydessä.

## Data classes

### Public product data

Julkista product dataa ovat käyttöliittymän julkiset tekstit, staattiset assetit ja ei-salaiset sovellusasetukset. Tätä saa commitoida repositoryyn, jos sisältö ei sisällä PII:tä, credentialeja, sisäisiä resursseja tai lisenssiehtojen alaista raakadataa.

### External source data

Ulkoisen lähteen dataa ovat EODHD-, YTJ- ja Inderes-lähteistä kerätyt tiedot. Tallennettuun dataan liitetään lähde, hakuajankohta ja lähteen oma tunniste, kun sellainen on saatavilla.

Ulkoista dataa ei saa tuotantokerätä ennen kuin lähteen käyttöehdot, lisenssi, robots-käytäntö, kutsurajat ja lähdemainintavaatimus on dokumentoitu.

### User PII

PII:tä ovat vähintään sähköposti, nimi, käyttäjätunnus, IP-osoite, requestiin liittyvä tunnistettava käyttäjäkonteksti ja admin-toimien kohteena oleva käyttäjä.

PII:tä saa tallentaa vain hyväksytyn käyttötapauksen tarvitsemassa laajuudessa. PII:tä ei saa lisätä lokiin, fixtureihin, virhevastauksiin tai domain-eventteihin ilman eksplisiittistä tarvetta ja sanitointia.

### Credentials and secrets

Credential- ja secret-luokkaan kuuluvat plaintext-salasanat, password hashit, tokenien plaintext-arvot, token-digestit, JWT:t, JWT-allekirjoitusavaimet, API-avaimet, webhook-salaisuudet, private keyt ja ulkoisten palvelujen tunnukset.

Credentialeja ja salaisuuksia ei saa commitoida, palauttaa API-vastauksessa, julkaista eventissä, tallentaa fixtureen tai lokittaa. Testeissä käytetään dummy-arvoja, jotka eivät muistuta oikeita avaimia.

### Operational logs and metrics

Lokit ja metriikat saavat sisältää request id:n, correlation id:n, bounded contextin, käyttötapauksen, ympäristön, tuloksen ja virheluokan. Lokit eivät saa sisältää salaisuuksia, tokeneita, credentialeja, plaintext-syötteitä tai ulkoisten palvelujen raw credential -arvoja.

## Retention and deletion

Auth-käyttäjän poisto koskee Auth bounded contextin käyttäjä-, credential- ja vahvistustietoja. Se ei määritä muiden bounded contextien poistoa, audit-retentiota tai anonymisointia.

Laajempi cross-context deletion, anonymisointi, audit trailin säilytys ja lakisääteinen retention vaativat erillisen päätöksen ennen tuotantototeutusta.

Kertakäyttöisten vahvistus- ja resetointisalaisuuksien plaintext-arvoa ei säilytetä. Digestillä, expiryllä ja used-tilalla voidaan todentaa käyttö ilman plaintext-arvon tallentamista.

## API and error handling

Käyttäjälle näkyvä virhe ei saa paljastaa sisäistä infrastruktuuria, AWS-resurssinimiä, credentialien olemassaoloa, token-digestin tilaa tai ulkoisen palvelun raakavirhettä.

Auth-kirjautumisen ja salasanan resetoinnin hylkäykset eivät saa paljastaa, onko käyttäjä olemassa, onko sähköposti vahvistettu, onko käyttäjä estetty tai oliko salasana väärä.

## Agent stop rules

Pysähdy ja pyydä päätös, jos:

- datan luokka on epäselvä
- muutos tallentaisi uuden PII- tai credential-kentän
- poistokäyttäytyminen vaikuttaa useaan bounded contextiin
- lokiin, eventtiin tai API-vastaukseen halutaan lisätä PII:tä tai credential-luonteista tietoa
- tuotantokeruu tarvitsee ulkoisen lähteen käyttöehtoja tai lisenssiehdon tulkintaa
- muutos voisi tuottaa sijoitusneuvontaa, osto- tai myyntisuosituksia tai automaattisen kaupankäyntipäätöksen

## Acceptance

- Agentti pystyy luokittelemaan uuden kentän ennen tallennusta.
- Agentti pystyy sanomaan, saako kenttä näkyä API-vastauksessa, eventissä, fixtureissä tai lokissa.
- Agentti pysähtyy cross-context deletion- ja retention-päätöksissä.
