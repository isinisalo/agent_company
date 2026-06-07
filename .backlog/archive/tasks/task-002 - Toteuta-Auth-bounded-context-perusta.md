---
id: TASK-002
title: Toteuta Auth bounded context -perusta
status: To Do
assignee: []
created_date: '2026-06-06 08:18'
updated_date: '2026-06-07 10:08'
labels:
  - Backend
  - Auth
milestone: m-1
dependencies: []
references:
  - .backlog/docs/intent/doc-001 - goal.md
priority: medium
ordinal: 1000
---

## Description

<!-- SECTION:DESCRIPTION:BEGIN -->
### MITÄ
Toteuta Auth bounded contextin yhteinen domain.

- Määritä `User`-aggregaatti, jolla on käyttäjän identiteetti, tilatiedot ja login-kelpoisuuden säännöt.
- Määritä Auth-domainin value objectit: `Email`, `Username`, `Password`, `EncryptedPassword`, `EmailVerificationToken`, `ResetPasswordToken` ja `Role`.
- Määritä usecasejen tarvitsemat portit: `IUserRepository`, `EventBus`, `SettingsStore` ja `PasswordHasher`.
- Määritä `DomainEvent`-perussopimus ilman credential-, token- tai secret-kenttiä.
- Varmista testeillä, että yhteisiä domain-sääntöjä voi käyttää kaikissa Auth-usecaseissa ilman päällekkäistä mallinnusta.

### MIKSI
Auth-usecaset tarvitsevat yhteisen käyttäjäidentiteetin, roolimallin, salasanakäsittelyn, token-digestien, tapahtumien ja repositorioporttien sopimuksen ennen kuin yksittäiset käyttötapaukset voidaan toteuttaa turvallisesti.
<!-- SECTION:DESCRIPTION:END -->

## Acceptance Criteria
<!-- AC:BEGIN -->
- [ ] #1 GIVEN Auth bounded context toteutetaan, WHEN `User`-aggregaatti määritetään, THEN se mallintaa käyttäjän identiteetin, tilan ja login-kelpoisuuden säännöt yhtenäisesti Auth-usecaseille.
- [ ] #2 GIVEN Auth value objecteja käytetään, WHEN `Email`, `Username`, `Password`, token-tyypit ja `Role` validoivat arvoja, THEN ne hyväksyvät vain sallitut arvot ja hylkäävät virheelliset arvot deterministisesti.
- [ ] #3 GIVEN usecase tarvitsee käyttäjien lukua tai muutosta, WHEN se riippuu `IUserRepository`-portista, THEN portti tukee `get_by_email`, `find_by_email`, `create`, `update`, `delete_by_email` ja `list_users` -operaatioita.
- [ ] #4 GIVEN Auth-usecase julkaisee domain-tapahtuman, WHEN `EventBus.publish` kutsutaan, THEN tapahtuma ei sisällä salasanoja, hasheja, tokeneita, token-digestejä, JWT:tä tai salaisuuksia.
- [ ] #5 GIVEN rekisteröinnin feature flag tarkistetaan, WHEN `SettingsStore.is_feature_enabled('/feature/auth/register_user')` kutsutaan, THEN se palauttaa boolean-arvon ja käsittelee puuttuvan, lukukelvottoman tai virheellisen arvon `false`-tuloksena.
- [ ] #6 GIVEN salasanan hash tai tarkistus tehdään, WHEN usecase käyttää salasanatoimintoja, THEN se riippuu `PasswordHasher`-portista eikä domain importtaa Argon2id- tai muuta hash-kirjastoa.
- [ ] #7 GIVEN Auth-perustaa validoidaan, WHEN testit ajetaan, THEN onnistuneet ja hylättävät value object -arvot, aggregate-siirtymät ja porttisopimukset on testattu ilman HTTP-, AWS- tai tietokantariippuvuutta.
<!-- AC:END -->



## Implementation Plan

<!-- SECTION:PLAN:BEGIN -->
Agentti täyttää tähän MITEN tehtävä toteutetaan käyttäjän määrittelemien kohtien MITÄ, MIKSI ja ESIMERKIT perusteella.

- [Toteutustapa]
- [Keskeiset tiedostot, rajapinnat tai komponentit]
- [Testaus- ja varmistustapa]
<!-- SECTION:PLAN:END -->

## Implementation Notes

<!-- SECTION:NOTES:BEGIN -->
Agentti kirjaa tähän toteutuksen aikaiset havainnot, päätökset ja mahdolliset poikkeamat suunnitelmasta.
<!-- SECTION:NOTES:END -->

## Final Summary

<!-- SECTION:FINAL_SUMMARY:BEGIN -->
Agentti kirjaa tähän loppuyhteenvedon, kun tehtävä on valmis.
<!-- SECTION:FINAL_SUMMARY:END -->

## Definition of Done
<!-- DOD:BEGIN -->
- [ ] #1 Käyttäjän määrittelemät Spec by Example -esimerkit on huomioitu toteutuksessa.
- [ ] #2 Toteutus on testattu tehtävän acceptance criteria -kohtia vasten.
- [ ] #3 Toteutuksen lopputulos ja mahdolliset rajaukset on kirjattu Final Summary -osioon.
<!-- DOD:END -->
