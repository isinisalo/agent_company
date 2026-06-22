---
id: adr-014
title: Valitaan Auth-kontekstin pysyvät turvallisuusrajat
date: '2026-06-22'
status: accepted
---
## Context
Auth-konteksti tarvitsee pysyvät turvallisuusrajat käyttäjän roolien, käyttötilan, vahvistustilan, enumeration-riskin ja poistamisen käsittelyyn. JWT-pohjainen API-autentikointi on päätetty ADR-010:ssä, mutta kaikki Auth-kontekstin pysyvät turvallisuusrajat eivät kuulu bearer-token-mallin päätökseen.

## Decision
Rekisteröityvä käyttäjä ei saa valita omaa rooliaan tai hallinnollista käyttötilaansa. Roolit ja hallinnolliset tilat määräytyvät hyväksytyn admin- tai käyttöoikeussopimuksen kautta.

Kirjautuminen, resetointipyyntö ja muut korkean enumeration-riskin virrat eivät saa paljastaa käyttäjän olemassaoloa silloin, kun paljastus kasvattaa väärinkäyttöriskiä.

Käyttäjän enable/disable-toiminto ei muuta sähköpostivahvistuksen tilaa. Admin-toiminto, joka kohdistuu puuttuvaan käyttäjään, ei saa luoda uutta käyttäjää implisiittisesti.

Käyttäjän poistaminen vaatii hyväksytyn deletion-, retention- ja compliance-rajan ennen pysyvää poistoa.

## Consequences

- Auth-use caset validoivat rooli- ja käyttötilamuutokset hyväksytyn hallintavirran kautta.
- Resetointi- ja kirjautumisvirtojen vastaukset suunnitellaan niin, ettei käyttäjäenumerointi vahvistu.
- Vahvistustila, käyttötila ja poistoprosessi ovat erillisiä käsitteitä, eikä yksi operaatio muuta toista ilman hyväksyttyä sopimusta.
- Puuttuva deletion-, retention- tai compliance-raja pysäyttää käyttäjän pysyvän poistamisen.
