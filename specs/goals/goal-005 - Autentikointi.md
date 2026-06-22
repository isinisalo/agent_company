---
id: goal-005
title: Autentikointi
type: other
created_date: '2026-06-07 12:35'
updated_date: '2026-06-22'
tags:
  - intent
  - goal
  - auth
---
# Autentikointi

## GOAL

Tarjoa turvallinen käyttäjäidentiteetin ja käyttöoikeuden perusta, jonka avulla palvelu voi erottaa rekisteröityneen käyttäjän, kirjautuneen käyttäjän ja hallintakäyttäjän.

## INTENT

Autentikoinnin tulee mahdollistaa palvelun käyttö ilman, että käyttäjän olemassaolo, salaisuudet tai arkaluonteinen käyttöoikeustieto vuotavat asiattomasti.

Muiden palvelun osien tulee voida luottaa siihen, että käyttäjän tunnistaminen, käyttötila ja roolit ovat selkeitä ja turvallisia.

## CAPABILITIES

- Käyttäjän rekisteröinti hyväksytyillä syötteillä ja turvallisilla oletusrooleilla.
- Kirjautuminen tunnisteella ja salasanalla, kun käyttäjä on kirjautumiskelpoinen.
- Sähköpostivahvistus kertakäyttöisellä ja vanhenevalla vahvistuksella.
- Salasanan resetointipyyntö, joka ei paljasta käyttäjän olemassaoloa.
- Salasanan resetoinnin vahvistus kertakäyttöisellä ja vanhenevalla salaisuudella.
- Hallintakäyttäjän käyttäjähallinta: käyttäjän käyttöönotto, käytöstä poisto, poisto ja listaus.

## EVIDENCE

Autentikointi etenee oikeaan suuntaan, kun käyttäjä voi rekisteröityä, kirjautua, vahvistaa sähköpostinsa, palauttaa salasanansa ja saada oikean käyttöoikeuden ilman arkaluonteisen tiedon vuotoa.
