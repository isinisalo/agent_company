---
id: TASK-002
title: Toteuta Auth bounded context -perusta
status: To Do
assignee: []
created_date: '2026-06-06 08:18'
updated_date: '2026-06-06 08:39'
labels:
  - Backend
  - Auth
milestone: m-1
dependencies: []
priority: medium
ordinal: 1000
---

## Description

<!-- SECTION:DESCRIPTION:BEGIN -->
### MITÄ
Toteuta Auth bounded contextin yhteinen perusta backendille.

- Määritä `User`-aggregaatin tila: name, email, password, verification_token, role, enabled ja last_login.
- Määritä Auth-domainin tyypit ja validointisäännöt: Email, Username, Password, EncryptedPassword, UnencryptedPassword, EmailVerificationToken, ResetPasswordToken ja Role.
- Määritä ja toteuta usecasejen tarvitsemat driven portit: `IUserRepository`, `EventBus` ja `SettingsStore`.
- Varmista, että Auth-usecaset voivat käyttää yhteisiä domain-sääntöjä ilman päällekkäistä mallinnusta.

### MIKSI
Kaikki Auth-usecaset käyttävät samaa User-aggregaattia, rooleja, validointisääntöjä ja repositorioportteja. Yhteinen perusta vähentää päällekkäisyyttä ja tekee usecase-toteutuksista yhdenmukaisia.
<!-- SECTION:DESCRIPTION:END -->

## Acceptance Criteria
<!-- AC:BEGIN -->
- [ ] #1 GIVEN Auth bounded context toteutetaan, WHEN domain-malli määritetään, THEN `User`-aggregaatilla on bc.md:n mukainen tila ja email-identiteetti.
- [ ] #2 GIVEN Auth-tyyppejä käytetään usecaseissa, WHEN syötteitä validoidaan, THEN Email, Username, Password ja Role noudattavat bc.md:ssä määriteltyjä sääntöjä.
- [ ] #3 GIVEN usecase tarvitsee käyttäjien lukua tai muutosta, WHEN se käyttää `IUserRepository`-porttia, THEN portti tukee get, find, create, update, delete ja list -operaatioita.
- [ ] #4 GIVEN rekisteröinti- tai resetointivirta julkaisee domain-tapahtuman, WHEN `EventBus.publish` kutsutaan, THEN se hyväksyy DomainEvent-sopimuksen mukaisen tapahtuman.
- [ ] #5 GIVEN rekisteröinnin feature flag tarkistetaan, WHEN `SettingsStore.is_feature_enabled` kutsutaan polulla `/feature/auth/register_user`, THEN se palauttaa boolean-arvon.
- [ ] #6 GIVEN Auth-perustaa muutetaan, WHEN toteutus validoidaan, THEN yhteiset domain-säännöt on testattu vähintään onnistuneilla ja hylättävillä arvoilla.
<!-- AC:END -->

## Definition of Done
<!-- DOD:BEGIN -->
- [ ] #1 Käyttäjän määrittelemät Spec by Example -esimerkit on huomioitu toteutuksessa.
- [ ] #2 Toteutus on testattu tehtävän acceptance criteria -kohtia vasten.
- [ ] #3 Toteutuksen lopputulos ja mahdolliset rajaukset on kirjattu Final Summary -osioon.
<!-- DOD:END -->
