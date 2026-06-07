---
id: goal-005
title: Auth bounded context goal
type: other
created_date: '2026-06-07 12:35'
updated_date: '2026-06-07 12:44'
tags:
  - intent
  - goal
  - auth
---
# Auth bounded context goal

## GOAL

Tarjoa turvallinen käyttäjäidentiteetin ja käyttöoikeuden perusta, jonka avulla selainkäyttöliittymä ja API voivat erottaa rekisteröityneen käyttäjän, kirjautuneen käyttäjän ja hallintakäyttäjän.

## INTENT

Auth-kontekstin tulee mahdollistaa palvelun käyttö ilman, että käyttäjän olemassaolo, credentialit, vahvistussalaisuudet tai tokenit vuotavat vastauksiin, tapahtumiin, fixtureihin tai lokiin.

Auth on jaettu peruskyvykkyys muille contexteille. Sen julkiset sopimukset saavat tarjota principalin, roolit, käyttötilan ja käyttäjäsummaryn, mutta eivät sisäisiä credential- tai token-malleja.

## CAPABILITIES

- Käyttäjän rekisteröinti hyväksytyillä syötteillä ja turvallisilla oletusrooleilla.
- Kirjautuminen tunnisteella ja salasanalla, kun käyttäjä on kirjautumiskelpoinen.
- Sähköpostivahvistus kertakäyttöisellä ja vanhenevalla vahvistuksella.
- Salasanan resetointipyyntö, joka ei paljasta käyttäjän olemassaoloa.
- Salasanan resetoinnin vahvistus kertakäyttöisellä ja vanhenevalla resetointisalaisuudella.
- Admin-käyttäjähallinta: käyttäjän käyttöönotto, käytöstä poisto, poisto ja listaus.

## CONSTRAINTS

- Älä tallenna, palauta, julkaise, lokita tai dokumentoi plaintext-salasanoja, vahvistussalaisuuksia, resetointisalaisuuksia, token-arvoja, token-digestejä, password hasheja, avaimia tai credentialeja.
- Älä paljasta käyttäjän olemassaoloa kirjautumisessa, resetointipyynnössä tai muussa virrassa, jossa se kasvattaa enumeration-riskiä.
- Älä anna rekisteröityvän käyttäjän valita rooliaan tai hallinnollista käyttötilaansa.
- Älä muuta sähköpostivahvistuksen tilaa käyttäjän enable/disable-toiminnossa.
- Älä luo uutta käyttäjää admin-toiminnossa, joka kohdistuu puuttuvaan käyttäjään.
- Pysähdy, jos deletion-, retention- tai compliance-sääntö puuttuu käyttäjän poistolle.

## EVIDENCE

Auth etenee oikeaan suuntaan, kun jokainen käyttötapaus on testattu onnistumis-, hylkäys-, idempotenssi-, authorization- ja salaisuuksien vuotamattomuustapauksilla domain/use case -rajassa ilman AWS-riippuvuuksia ja adapterit mockeilla silloin, kun adapterit toteutetaan.
