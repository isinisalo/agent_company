---
id: decision-009
title: '[Backend] Valitaan Auth domain-malli'
date: '2026-06-07 10:54'
status: accepted
---
## Context

Auth-konteksti tarvitsee yhtenäisen domain-kielen ennen kirjautumisen, rekisteröinnin, sähköpostivahvistuksen, salasanan resetoinnin ja admin-käyttäjähallinnan toteutusta.

Ilman yhteistä päätöstä yksittäiset käyttötapaukset joutuisivat itse päättämään käyttäjän tilat, roolit, kirjautumiskelpoisuuden, salasanakäsittelyn, kertakäyttöisten salaisuuksien elinkaaren ja domain-tapahtumien tietoturvarajat.

Auth-domainin tulee pysyä riippumattomana HTTP:stä, AWS:stä, DynamoDB:stä, Pydanticista, PynamoDB:stä, PyJWT:stä, boto3:sta ja viestintäpalvelujen toteutuksista.

## Decision

Auth omistaa käyttäjän identiteetin, credential-tiedot, kirjautumiskelpoisuuden, sähköpostivahvistuksen, salasanan resetoinnin, roolin ja hallinnollisen käyttötilan.

Käyttäjällä on muuttumaton sisäinen käyttäjätunniste, kanonisoitu sähköposti, käyttäjänimi, rooli, sähköpostivahvistuksen tila, hallinnollinen käyttötila, salasanan tarkistamiseen tarvittava tallennettu tieto sekä metatiedot luonnista ja päivityksistä.

Sähköposti on käyttäjän yksilöllinen kirjautumistunniste. Sähköposti kanonisoidaan ennen vertailua ja tallennusta. Käyttäjänimi on näyttö- ja hallintanimi, ei credential eikä roolin lähde.

Roolit ovat `user` ja `admin`. Rekisteröityvä käyttäjä saa aina roolin `user`. Roolia ei voi valita rekisteröintipyynnössä. Roolin muuttaminen vaatii erillisen admin-käyttötapauksen tai uuden hyväksytyn tehtävän.

Sähköpostivahvistuksen tilat ovat `unverified` ja `verified`. Hallinnollisen käyttötilan tilat ovat `enabled` ja `disabled`. Nämä tilat ovat erillisiä. Sähköpostivahvistus ei saa muuttaa hallinnollista käyttötilaa, eikä admin-käyttötilan muutos saa muuttaa sähköpostivahvistuksen tilaa.

Käyttäjä on kirjautumiskelpoinen vain, kun kaikki ehdot täyttyvät:

- käyttäjä on olemassa
- sähköposti on `verified`
- hallinnollinen käyttötila on `enabled`
- salasana täsmää tallennettuun salasanatietoon

Kirjautumisen hylkäys ei saa paljastaa, mikä ehto epäonnistui.

Salasana on plaintext-arvo vain sisääntulevan komennon käsittelyn ajan. Domain ei tallenna plaintext-salasanaa eikä tunne hash-kirjastoa. Salasanan tallennettu tieto on credential-luokan dataa ja sitä saa käsitellä vain salasanaportin ja persistenssiadapterin kautta.

Salasanan vähimmäispituus on 12 merkkiä ja enimmäispituus 128 merkkiä. Tyhjää tai pelkistä whitespace-merkeistä koostuvaa salasanaa ei hyväksytä. Koostumussääntöjä ei lisätä ilman erillistä security-päätöstä.

Sähköpostivahvistuksen ja salasanan resetoinnin salaisuudet ovat kertakäyttöisiä. Plaintext-salaisuus saa olla olemassa vain käyttötapauksen muistissa niin kauan kuin se tarvitaan toimituspyynnön muodostamiseen. Tallennetaan vain digest, expiry ja käytön tila tai käytön aikaleima.

Sähköpostivahvistuksen oletusvoimassaoloaika on 24 tuntia. Salasanan resetoinnin oletusvoimassaoloaika on 60 minuuttia. Arvot luetaan konfiguraatiosta, ja puuttuva tai virheellinen arvo ei saa johtaa turvallisuudeltaan heikompaan oletukseen tuotannossa.

Käyttötapaus saa pyytää Notifications-kontekstia toimittamaan vahvistus- tai resetointiviestin. Domain-tapahtumat eivät saa sisältää plaintext-salaisuutta, salasanaa, password hashia, token-digestiä, JWT:tä tai API-avainta.

Auth-domainin tapahtumat saavat sisältää vain käyttötapauksen kannalta välttämättömän tunniste- ja tilatiedon. Tapahtumat eivät ole ilmoituskanavan credential-kuljetus.

## Consequences

- Käyttötapaukset viittaavat samaan kirjautumiskelpoisuuden sääntöön eivätkä toista tilalogiikkaa eri tavoin.
- Rekisteröinti luo käyttäjän roolilla `user`, sähköpostitilalla `unverified` ja hallinnollisella käyttötilalla `enabled`.
- Adminin enable- ja disable-toiminnot ovat idempotentteja ja muuttavat vain hallinnollista käyttötilaa.
- Sähköpostivahvistus kuluttaa vahvistussalaisuuden ja muuttaa vain sähköpostivahvistuksen tilaa.
- Salasanan resetoinnin pyyntö ei paljasta käyttäjän olemassaoloa.
- Salasanan resetoinnin vahvistus vaihtaa salasanan vain oikealla, voimassa olevalla ja käyttämättömällä resetointisalaisuudella.
- Domain-testien tulee kattaa validit ja hylättävät sähköpostit, käyttäjänimet, salasanat, tilasiirtymät, kirjautumiskelpoisuus ja salaisuuksien vuotamattomuus.
- Notifications-tuotantolähetys pysyy erillisenä päätöksenä. Auth voi toteuttaa portin ja testituplat ilman tuotantotoimituskanavaa.
- Jos tulevaisuudessa tarvitaan roolinmuutos, refresh tokenit, token revocation, tililukitus, MFA tai cross-context deletion, niistä tehdään erillinen tehtävä tai ADR.
