---
id: decision-008
title: Valitaan JWT-pohjainen API-autentikointi
date: '2026-06-06'
status: accepted
---
## Context
Backend tarvitsee stateless-tavan välittää autentikoidun käyttäjän identiteetti API-kutsuihin ilman palvelinpuolen sessiomuistia.

## Decision
JWT-tokenit valitaan backendin API-autentikoinnin bearer-token-malliksi. API-reuna validoi tokenin ja rakentaa validista tokenista eksplisiittisen `Principal`-olion, joka välitetään use caseille ja auktorisointilogiikalle.

## Consequences

- JWT:t välitetään ensisijaisesti `Authorization: Bearer <token>` -headerissa.
- Tokenin allekirjoitus, expiration, issuer, audience ja vaaditut claimit tarkistetaan ennen use case -kutsua.
- Domain ja application eivät saa importata JWT-kirjastoa, lukea HTTP-headereita tai käsitellä raakaa tokenia.
- JWT-salaisuudet, yksityiset avaimet ja issuer-konfiguraatio säilytetään Secrets Managerissa tai hyväksytyssä turvallisessa konfiguraatiopalvelussa.
- Tokenia tai salaisia avaimia ei saa lokittaa.
- Refresh-tokenien, revokoinnin ja tokenin elinkaaren yksityiskohdat vaativat erillisen hyväksytyn auth-spesifikaation tai tehtävän.
