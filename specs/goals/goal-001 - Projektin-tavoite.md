---
id: goal-001
title: Projektin tavoite
type: other
created_date: '2026-06-06 07:19'
updated_date: '2026-06-22'
tags:
  - intent
  - goal
---
# Projektin tavoite

## GOAL

Rakenna selainkäyttöinen palvelu, jossa käyttäjä voi seurata suomalaisia yrityksiä ja nähdä samassa näkymässä yrityksen perustiedot, markkinadatan, yritykseen liittyvän keskusteluaineiston ja tiedonkeruun tilan.

Palvelun onnistunut lopputila on, että seurattava yritys lisätään järjestelmään kerran, minkä jälkeen järjestelmä kerää, tallentaa, attribuoi ja näyttää yritykseen liittyvän tiedon ilman, että käyttäjän täytyy hakea sama tieto käsin erillisistä lähteistä.

## INTENT

Agenttien tulee tehdä ratkaisuja kohti keskitettyä yritysseurantapalvelua, ei yleistä CRM:ää, sijoitusneuvontatyökalua, yritysrekisteriä tai sosiaalisen median keräintä.

Palvelun tulee priorisoida jäljitettävää tiedonkeruuta, lähdeattribuutiota, turvallista käyttäjähallintaa ja hallittua siirtymää oikeaan tuotantokäyttöön.

## PRODUCT SCOPE

Järjestelmän tavoitealueet ovat:

- Autentikointi: käyttäjän rekisteröinti, kirjautuminen, sähköpostivahvistus, salasanan resetointi ja hallintakäyttäjän käyttäjähallinta.
- Viestintä: käyttäjälle tarkoitettujen viestien muodostaminen, kirjaaminen ja toimitustilan näyttäminen.
- Yritysseuranta: seurattavat yritykset, yritysten perustiedot ja käyttäjän seuranta-asetukset.
- Markkinadata: seurattavien yritysten markkinadatan haku, yhdenmukaistaminen, tallennus ja näyttäminen.
- Keskusteluaineisto: yrityksiin liittyvän keskusteluaineiston haku, deduplikointi, tallennus ja näyttäminen.
- Tiedonkeruun ajastus: yrityskohtaisten tiedonkeruiden ajastaminen, tilan näyttäminen ja puutteellisesti hyväksytyn tuotantokeruun estäminen.

Osa-alueiden tavoitteet ovat näissä dokumenteissa:

- `specs/goals/goal-004 - Projektin-ohjaus.md`
- `specs/goals/goal-005 - Autentikointi.md`
- `specs/goals/goal-006 - Viestinta.md`
- `specs/goals/goal-007 - Yritysseuranta.md`
- `specs/goals/goal-008 - Markkinadata.md`
- `specs/goals/goal-009 - Keskusteluaineisto.md`
- `specs/goals/goal-010 - Tiedonkeruun-ajastus.md`

## PRODUCT LIMITS

- Järjestelmä ei tuota sijoitusneuvontaa, osto- tai myyntisuosituksia, automaattisia kaupankäyntipäätöksiä eikä kaupankäyntitoiminnallisuutta.
- Reaaliaikainen jatkuva markkinadatavirta ei kuulu alkuvaiheen tavoitteeseen.

## EVIDENCE

Tavoite etenee oikeaan suuntaan, kun seurattavan yrityksen lisääminen, tiedon keruu, lähdeattribuoitu tallennus, selaimessa näkyvä koontinäkymä, käyttäjän turvallinen käyttöoikeus ja hallittu tuotantokäytön rajaus toimivat ilman arkaluonteisen tiedon vuotoa.
