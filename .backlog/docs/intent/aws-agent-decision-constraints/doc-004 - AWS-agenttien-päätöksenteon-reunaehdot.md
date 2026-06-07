---
id: doc-004
title: AWS-agenttien päätöksenteon reunaehdot
type: specification
created_date: '2026-06-07 06:33'
tags:
  - intent
  - aws
  - agents
  - constraints
---
# AWS-agenttien päätöksenteon reunaehdot

## Tarkoitus

Tämä speksi täydentää dokumenttia `.backlog/docs/intent/goal.md`. Sen tehtävä on antaa agenteille riittävä päätöksentekokehys AWS-pohjaisen web-sovelluksen toteuttamiseen silloin, kun yksityiskohtainen käyttötapaus-, API-, data- tai infrastruktuurispeksi puuttuu.

Agentti saa tehdä itsenäisiä päätöksiä vain tämän dokumentin, hyväksyttyjen arkkitehtuuripäätösten, Backlog-tehtävän ja olemassa olevan koodin muodostamassa rajassa. Jos päätös muuttaisi projektin tavoitetta, hyväksyttyä arkkitehtuuria, tietoturvamallia, kustannusprofiilia tai julkista sopimusta olennaisesti, agentti ei saa ratkaista asiaa oletuksella vaan sen tulee pyytää hyväksyntä tai kirjata uusi ADR-/speksehdotus.

## Mitä `goal.md`:n lisäksi tarvitaan

Agenttien itsenäinen työ edellyttää, että projektissa on vähintään seuraavat dokumenttityypit tai niiden puuttuessa tässä speksissä määritelty oletuslinja:

1. Hyväksytyt arkkitehtuuripäätökset: AWS serverless -alusta, DynamoDB, backend-arkkitehtuuri, runtime, autentikointi, frontend ja CI/CD ovat päätöksiä, joita agentti ei saa ohittaa ilman uutta hyväksyttyä päätöstä.
2. Bounded context -kuvaukset: kunkin kyvykkyyden vastuut, termit, aggregate-rajat, invarianssit ja ulkoiset portit.
3. Käyttötapausspeksit: hyväksytyt komennot, kyselyt, roolit, virheet, auditointitarpeet ja käyttäjälle näkyvä lopputulos.
4. API-sopimukset: endpointit, request/response-mallit, virhekoodit, autentikointi, authorisointi, CORS ja versiointi.
5. DynamoDB access pattern -speksit: avaimet, indeksit, kyselyt, kirjoitusmallit, TTL, ehdolliset kirjoitukset ja kapasiteettiolettamat.
6. AWS-resurssispeksit: Lambda-funktiot, API Gateway -reitit, EventBridge-säännöt, DynamoDB-taulut, IAM-roolit, Parameter Store -parametrit, Secrets Manager -salaisuudet, CloudWatch-lokit ja hälytykset.
7. Konfiguraatio- ja salaisuuskatalogi: mitä arvoja on olemassa, missä ne sijaitsevat, mikä saa lukea ne, miten ne nimetään ja mitkä arvot ovat ympäristökohtaisia.
8. Operointiohjeet: deploy-, rollback-, smoke test-, lokitus-, hälytys- ja incident-käytännöt.
9. Tietoturva- ja dataluokittelu: henkilötiedot, tunnistetiedot, ulkoisten lähteiden data, säilytysajat ja lokitusrajoitukset.
10. Testausstrategia: mitkä asiat testataan yksikkö-, adapteri-, sopimus-, integraatio- ja end-to-end-tasolla.

Jos jokin yllä olevista puuttuu, agentti saa tehdä vain vähäriskisen, palautettavan ja olemassa oleviin päätöksiin sopivan oletuspäätöksen tämän dokumentin mukaan.

## Päätöshierarkia

Agentin tulee ratkaista epäselvyydet seuraavassa järjestyksessä:

1. Käyttäjän tai tehtävän eksplisiittinen vaatimus.
2. `goal.md` ja projektin rajaukset.
3. Hyväksytyt päätökset `.backlog/decisions/`-hakemistossa.
4. Olemassa oleva koodi, testit, nimeämiskäytännöt ja hakemistorakenne.
5. Tämä speksi.
6. AWS:n, Pythonin, FastAPI:n, DynamoDB:n ja Reactin vakiintuneet hyvät käytännöt.

Alempi taso ei saa kumota ylemmän tason päätöstä. Jos olemassa oleva koodi on ristiriidassa hyväksytyn päätöksen kanssa, agentti saa korjata paikallisen toteutuksen päätöksen mukaiseksi vain, jos se kuuluu tehtävän rajaukseen. Muussa tapauksessa agentti kirjaa löydöksen ja ehdottaa jatkotehtävää.

## Päätökset, jotka agentti saa tehdä itse

Agentti saa tehdä seuraavat päätökset ilman erillistä hyväksyntää, kun ne ovat tehtävän kannalta tarpeellisia ja pysyvät hyväksytyissä arkkitehtuurirajoissa:

- Valita yksinkertaisimman toteutustavan, joka täyttää käyttötapauksen eikä lisää uutta palvelua, kirjastoa tai julkista sopimusta.
- Lisätä tai muuttaa testejä, mockeja, fixturejä ja paikallisia adapteritestirakenteita.
- Nimetä Lambda-handlerit, parametrit, salaisuudet, DynamoDB-attribuutit ja sisäiset moduulit olemassa olevan nimeämistavan mukaan.
- Lisätä ei-salaisia ympäristökohtaisia konfiguraatioarvoja Parameter Storeen, kun arvo tarvitaan deployattavan toiminnon käynnistymiseen.
- Lisätä tarvittavan vähäoikeuksisen IAM-luvan tietylle funktiolle ja resurssille, kun lupa on suoraan pääteltävissä tehtävän hyväksymiskriteereistä.
- Valita kohtuulliset aikakatkaisut, retry-rajat, lokikentät ja metriikat, kun tarkempaa operointispeksiä ei ole.
- Tehdä DynamoDB-tietomalliin käyttötapauksen edellyttämän uuden attribuutin tai indeksiehdotuksen, kun access pattern on selkeä ja muutos ei riko olemassa olevia käyttötapauksia.
- Toteuttaa adapterin ulkoiselle palvelulle mockattavana porttina ilman tuotantokäyttöönottoa, jos lähteen lisenssi- tai käyttöehtotarkistus on kesken.

## Päätökset, joissa agentin tulee pysähtyä

Agentti ei saa tehdä seuraavia päätöksiä itsenäisesti:

- Uuden AWS-palvelun lisääminen hyväksyttyjen palvelujen ulkopuolelta.
- Monorepon top-level-rakenteen, CI/CD-mallin, runtime-version, backend-arkkitehtuurin tai frontend-teknologian muuttaminen.
- Tuotantoresurssien luominen, poistaminen, migraatio tai deploy ilman tehtävän eksplisiittistä deploy-scopea.
- IAM-wildcardien lisääminen laajasti, kuten `Action: *`, `Resource: *` tai usean palvelun kattavat hallintaoikeudet.
- Julkisen endpointin, uuden autentikointimallin, refresh-token-mallin, käyttäjäroolimallin tai authorisointisäännön muuttaminen ilman auth-speksejä.
- DynamoDB:n avainrakenteen tai pääindeksin muuttaminen tavalla, joka voi rikkoa olemassa olevan datan tai kyselyt.
- Salaisuuksien tallennuspaikan, kierrätysmallin tai avainmateriaalin muutos ilman tietoturvapäätöstä.
- Ulkoisen datalähteen tuotantokäyttö, jos käyttöehdot, robots-käytännöt, lisenssi tai lähdemainintavaatimus on epäselvä.
- Ratkaisu, joka voi tuottaa sijoitusneuvontaa, kaupankäyntisuosituksia tai automaattisia kaupankäyntipäätöksiä.
- Päätös, joka kasvattaa pysyviä kustannuksia merkittävästi, kuten provisioned-kapasiteetti, jatkuvasti ajettava compute, laaja lokiretention kasvu tai monialueinen arkkitehtuuri.

## Yleiset AWS-reunaehdot

AWS-infrastruktuurin lähde on versionhallittu infrastruktuurikoodi, ensisijaisesti AWS SAM -template. Agentti ei saa tehdä pysyviä manuaalisia konsolimuutoksia osaksi ratkaisua.

Ympäristöt tulee erottaa nimissä, parametreissa, salaisuuksissa, IAM-rooleissa ja resursseissa. Oletusympäristöt ovat `dev`, `test` ja `prod`, ellei infra-spekseissä toisin määrätä. Koodi ei saa kovakoodata ympäristöä, tilin tunnuksia, alueita, ARNeja, salaisuuksia tai taulunimiä.

Resurssit nimetään johdonmukaisesti muodolla, josta käy ilmi sovellus, ympäristö, bounded context ja vastuu. Jos vakiota ei ole, käytä kaavaa `<app>-<env>-<context>-<purpose>` infrastruktuurissa ja Parameter Store -poluissa kaavaa `/<app>/<env>/<context>/<name>`.

Kaikki tuotantoon vaikuttavat resurssit tulee tagittaa vähintään sovelluksella, ympäristöllä, omistajuudella ja kustannusseurannalla, jos tagit ovat infrastruktuurimallissa käytössä.

Pitkäikäisiä AWS access key -avaimia ei saa lisätä repositoryyn, CI/CD:hen tai dokumentaatioon. GitHub Actions -julkaisut käyttävät ensisijaisesti OIDC-pohjaista luottamusta.

## Lambda

Lambda-funktiot ovat tilattomia. Pysyvä tila tallennetaan DynamoDB:hen tai muuhun hyväksyttyyn palveluun, ei prosessin muistiin, `/tmp`-hakemistoon tai globaaleihin muuttujiin.

Funktiot saavat alustaa AWS-clientit ja muut raskaat riippuvuudet moduulitasolla kylmäkäynnistyksen vähentämiseksi, mutta ne eivät saa alustuksessa lukea käyttäjäkohtaista tilaa tai tehdä peruuttamattomia sivuvaikutuksia.

FastAPI julkaisee HTTP-rajapinnat ja Mangum rajataan Lambda-ASGI-entrypointtiin. Lambda-handler ei saa sisältää domain-logiikkaa, vaan sen tulee koostaa ulkokerrokset, validaatio ja use case -kutsu.

Lambda-timeout asetetaan mahdollisimman pieneksi realistiseen käyttötapaukseen nähden. Ulkoisille HTTP-kutsuille tulee aina olla erillinen request-timeout, joka on selvästi Lambda-timeoutia pienempi. Agentti ei saa jättää ulkoista kutsua ilman aikakatkaisua.

Tausta-ajot ja EventBridge-käsittelijät toteutetaan idempotenteiksi. Sama tapahtuma saa tulla useammin kuin kerran ilman, että data korruptoituu tai käyttäjälle syntyy tuplavaikutus.

Ulkoisiin API-lähteisiin kohdistuvat Lambdat rajoittavat rinnakkaisuutta ja retryjä niin, ettei lähteen kutsurajoja tai käyttöehtoja rikota. Jos rajoja ei tunneta, agentti valitsee konservatiivisen oletuksen ja tekee rajan konfiguroitavaksi.

Asynkronisille käsittelijöille tulee määritellä retry-, DLQ- tai muu virheiden talteenottomalli silloin, kun epäonnistuminen ei ole käyttäjälle välittömästi näkyvä ja uudelleenajo on mahdollinen.

## API Gateway, CloudFront ja HTTP

Julkinen HTTP-liikenne kulkee API Gatewayn kautta Lambda-funktioille ja frontend CloudFrontin kautta staattisena SPA-sovelluksena. Uutta julkista reittiä ei saa lisätä ilman autentikointi-, authorisointi- ja CORS-vaikutusten arviointia.

CORS tulee määritellä eksplisiittisesti sallittuihin originiin. Wildcard-originia ei käytetä autentikoiduille reiteille.

API-virheet palautetaan vakaassa muodossa, joka ei paljasta sisäisiä poikkeuksia, salaisuuksia, AWS-resurssinimiä tai ulkoisten palvelujen raakoja virheitä. Sisäinen virhe saa näkyä lokeissa vain sanitisoituna.

JWT bearer -autentikointi validoidaan API-reunalla. Domain ja application-kerros saavat vain eksplisiittisen `Principal`-olion, eivät raakaa tokenia, HTTP-headeria tai JWT-kirjaston mallia.

## DynamoDB

DynamoDB-malli suunnitellaan access pattern -lähtöisesti. Normaali käyttöliikenne ei saa perustua tauluskannauksiin, ad hoc -relaatiokyselyihin tai filttereihin, jotka lukevat laajasti dataa ja hylkäävät suurimman osan tuloksista sovelluksessa.

Jos tarkempaa tietomallipäätöstä ei ole, agentti valitsee bounded context -kohtaisen taulun ja dokumentoi tärkeimmät kyselyt. Single-table-mallin saa valita vain, jos saman bounded contextin access patternit, avainmalli ja item-tyypit on kuvattu riittävästi.

Pääavaimet ja GSI:t nimetään käyttötapauksen mukaan. Indeksi lisätään vain, kun sille on selkeä kyselytarve. Indeksiä ei saa lisätä varmuuden vuoksi.

Kirjoituksissa käytetään ehdollisia operaatioita, kun luodaan yksilöllisiä resursseja, estetään päällekkäisiä tapahtumia tai suojataan optimistisella lukituksella. Idempotency key tallennetaan, kun sama komento tai tapahtuma voi tulla uudelleen.

Ajat tallennetaan UTC-aikaan ISO 8601 -muodossa, ellei käyttötapaus vaadi muuta. Rahamäärissä, hinnoissa ja tarkoissa numeerisissa arvoissa ei käytetä binäärisiä liukulukuja.

Ulkoisesta lähteestä tallennettuun dataan liitetään lähde, hakuajankohta ja tarvittaessa lähteen oma tunniste. Agentti ei saa hävittää lähdeattribuuttia mallista, jos data on peräisin EODHD:stä, Inderes Forumista tai YTJ:stä.

Tuotantotauluille oletetaan Point-in-Time Recovery ja hallittu salaus, ellei infra-spekseissä ole perusteltua poikkeusta. TTL otetaan käyttöön vain datalle, jonka säilytysajan käyttötapaus tai turvallisuusmalli määrittelee.

## Secrets Manager

Secrets Manager on ensisijainen paikka API-avaimille, JWT-allekirjoitusavaimille, yksityisille avaimille, webhook-salaisuuksille, ulkoisten palvelujen tunnuksille ja muille arvoille, joiden paljastuminen aiheuttaisi tietoturvariskin.

Salaisuuksia ei saa tallentaa Git-repositoryyn, SAM-templatejen plaintext-arvoihin, `.env`-esimerkkeihin, lokiin, testifixtureihin tai virheviesteihin. Testeissä käytetään dummy-arvoja, jotka eivät muistuta oikeita avaimia.

Lambda saa lukea vain ne salaisuudet, joita sen käyttötapaus tarvitsee. IAM-policy rajataan salaisuuden ARNiin tai hyväksyttyyn nimiprefixiin. Laaja `secretsmanager:*` tai kaikki salaisuudet kattava lukuoikeus ei ole hyväksyttävä oletus.

Salaisuudet luetaan käynnistyksessä tai välimuistitetaan prosessin eliniän ajaksi vain, jos se ei estä kierrätystä kohtuuttomasti. Jos salaisuudelle on rotaatiomalli, toteutuksen tulee sietää salaisuuden vaihtuminen ilman koodimuutosta.

Jos arvo voi olla sekä konfiguraatio että salaisuus, agentti luokittelee sen salaisuudeksi, kunnes toisin päätetään.

## Parameter Store

Parameter Storeen tallennetaan ei-salainen, ympäristökohtainen konfiguraatio: taulunimet, endpointit, feature flagit, kutsurajat, aikakatkaisut, polling-välit, sallittujen originien listat ja muut arvot, joiden paljastuminen ei itsessään vaaranna järjestelmää.

Parameter Store -polut ovat ympäristö- ja context-kohtaisia. Oletuskaava on `/<app>/<env>/<context>/<name>`. Parametrin nimestä tulee käydä ilmi käyttötarkoitus ilman, että arvoa tarvitsee lukea.

Koodi ei saa hiljaisesti käyttää tuotantoon sopimattomia oletusarvoja, jos parametri puuttuu. Puuttuva pakollinen parametri aiheuttaa käynnistys- tai käyttötapauskohtaisen virheen, joka kertoo parametrin nimen mutta ei sisällä salaisia arvoja.

SecureString-parametria saa käyttää vain hyväksytyn infra- tai tietoturvalinjauksen perusteella. Lähtökohtaisesti salaisuudet kuuluvat Secrets Manageriin ja ei-salaiset asetukset Parameter Storeen.

## IAM

IAM-oikeudet toteutetaan least privilege -periaatteella. Jokaisella Lambda-funktiolla tai pienellä funktioryhmällä tulee olla rooli, joka sallii vain sen tarvitsemat toiminnot tiettyihin resursseihin.

Agentti saa lisätä IAM-luvan, kun kaikki seuraavat ehdot täyttyvät: käyttötapaus tarvitsee luvan, resurssi on yksilöitävissä, action on rajattavissa ja muutos voidaan testata. Jos jokin ehto ei täyty, agentti ei saa paikata ongelmaa wildcardilla.

IAM-policyssä käytetään resurssikohtaisia ARNeja ja tarvittaessa ehtoja. Wildcard on sallittu vain, jos AWS-palvelu ei tue resurssirajausta kyseiselle actionille, ja tällöin syy dokumentoidaan kommenttiin tai päätökseen.

CI/CD-roolit eivät saa periä sovelluksen runtime-rooleja. Deploy-oikeudet, runtime-oikeudet ja paikalliskehityksen oikeudet pidetään erillään.

## EventBridge ja ajastukset

Ajastettu tiedonkeruu toteutetaan EventBridgellä hyväksytyn alustan mukaisesti. Ajastusväli pidetään konservatiivisena, jos lähteen kutsurajoja tai liiketoimintatarvetta ei ole määritelty.

Ajastettu käsittelijä ei saa olettaa, että edellinen ajo onnistui. Sen tulee pystyä jatkamaan viimeisestä tunnetusta tilasta, ohittamaan jo käsitelty data ja kirjaamaan epäonnistumiset uudelleenajettavalla tavalla.

Event payload ei saa sisältää salaisuuksia. Tapahtumiin tallennetaan vain käsittelyn kannalta tarpeellinen tunniste- ja kontekstitieto.

## Lokitus, metriikat ja hälytykset

Lokien tulee olla rakenteisia. Vähimmäiskenttiä ovat request id tai correlation id, käyttötapaus, bounded context, ympäristö, tulos ja virheen luokka. Henkilötietoja, tokenia, salaisuuksia, API-avaimia tai ulkoisten palvelujen raw credential -arvoja ei saa lokittaa.

Agentti saa lisätä metriikoita ja hälytyksiä kriittisiin virtoihin, erityisesti autentikointiin, ajastettuun tiedonkeruuseen, ulkoisten API:en virheisiin, DynamoDB conditional check -epäonnistumisiin ja Lambda-timeoutteihin.

Virheilmoitusten tulee erottaa käyttäjälle näkyvä viesti ja sisäinen diagnostiikka. Käyttäjälle näkyvä viesti ei saa paljastaa sisäistä infrastruktuuria tai salaisuuksia.

Lokien retention asetetaan ympäristökohtaisesti. Jos retention-speksejä ei ole, agentti valitsee lyhyen retentionin dev/test-ympäristöihin ja pidemmän, mutta kustannuksiltaan rajatun retentionin tuotantoon.

## Tietoturva, data ja regulaatio

Käyttäjädata, autentikointidata ja admin-toiminnot käsitellään vähimmän tiedon periaatteella. Käyttötapaus saa pyytää ja tallentaa vain datan, jota se tarvitsee.

Ulkoisten datalähteiden dataan liittyvät käyttöehdot, robots-käytännöt, lisenssit ja lähdemainintavaatimukset tulee tarkistaa ennen tuotantokäyttöä. Jos tarkistus puuttuu, agentti saa toteuttaa rajapinnan, mockin ja testit mutta ei tuotantokeruuta.

Poisto- ja säilytyskäytännöissä agentti ei saa arvata lakisääteisiä velvoitteita. Jos henkilötiedon poistaminen, anonymisointi tai audit trail on epäselvä, agentti toteuttaa teknisen valmiuden eriytettynä ja pyytää hyväksynnän varsinaiselle politiikalle.

## Kustannus- ja kapasiteettiperiaatteet

Oletusvalinta on serverless ja käytön mukaan skaalautuva kapasiteetti. DynamoDB:n oletus on on-demand-kapasiteetti, ellei liikennemäärästä ja kustannusmallista ole hyväksyttyä päätöstä.

Agentti ei saa ottaa käyttöön provisioned-kapasiteettia, monialueista aktiivista replikointia, jatkuvasti ajettavaa compute-resurssia tai pitkää lokiretentionia ilman kustannusperustelua ja hyväksyntää.

Ulkoisten API:en kutsut rajoitetaan konfiguroitavilla rajoilla. Jos kutsurajoja ei tunneta, agentti käyttää konservatiivista oletusta ja dokumentoi sen.

Resurssit suunnitellaan niin, että dev/test-ympäristöt voidaan ajaa pienillä kustannuksilla. Testiympäristö ei saa oletusarvoisesti käynnistää laajaa ajastettua keruuta.

## Testaus ja paikalliskehitys

Domain- ja use case -testit eivät saa riippua AWS:stä. AWS-adapterit testataan ensisijaisesti motolla tai rajatuilla mockeilla. Ulkoiset HTTP-integraatiot testataan responses-kirjastolla tai Mockoonilla hyväksyttyjen päätösten mukaan.

Tuotantoresursseihin kohdistuvia testejä ei ajeta oletuksena. Deployn jälkeiset smoke testit saa ajaa vain tehtävän deploy-scopeen kuuluvassa ympäristössä ja ilman todellisia salaisuuksia tai käyttäjädataa lokittavia tarkistuksia.

Testien tulee todentaa myös virhepolut: puuttuva parametri, puuttuva salaisuus, väärä IAM-oikeus mockattuna, DynamoDB conditional failure, ulkoisen API:n timeout ja idempotentti uudelleenajo silloin, kun nämä liittyvät toteutettavaan käyttötapaukseen.

## Oletuspäätökset puuttuvan speksin tilanteissa

Kun tarkempi speksi puuttuu, agentti käyttää seuraavia oletuksia:

- Valitse ratkaisu, joka on pienin, palautettava ja sopii hyväksyttyihin päätöksiin.
- Älä lisää uutta AWS-palvelua, kirjastoa, top-level-hakemistoa tai julkista API-sopimusta ilman hyväksyntää.
- Pidä domain riippumattomana AWS:stä, HTTP:stä, Pydanticista, PynamoDB:stä, boto3:sta ja JWT-kirjastosta.
- Käytä Parameter Storea ei-salaiselle konfiguraatiolle ja Secrets Manageria salaisuuksille.
- Käytä DynamoDB:ssä kyselypohjaista avainmallia ja vältä runtime-scanneja.
- Käytä Lambda-funktioissa aikakatkaisuja, idempotenssia ja rajattua retry-mallia.
- Käytä IAM:ssa resurssikohtaisia least privilege -lupia.
- Lisää testit sille tasolle, jolla päätös voidaan todentaa ilman oikeaa AWS-tuotantoympäristöä.
- Dokumentoi oletus tehtävän muistiinpanoihin tai speksiin, jos oletus vaikuttaa tulevien agenttien päätöksiin.
- Pyydä hyväksyntä, jos päätöksellä on pysyvä tietoturva-, kustannus-, data-, deploy- tai julkisen sopimuksen vaikutus.

## Agentin tarkistuslista ennen muutosta

Ennen toteutusta agentin tulee varmistaa:

- Onko tehtävä sidottu olemassa olevaan Backlog-tehtävään ja hyväksyttyyn suunnitelmaan?
- Mihin bounded contextiin muutos kuuluu?
- Muuttaako ratkaisu hyväksyttyjä ADR-päätöksiä?
- Tarvitaanko uutta AWS-resurssia vai riittääkö olemassa oleva resurssi?
- Mitä IAM-oikeuksia Lambda tarvitsee ja voiko ne rajata resurssiin?
- Onko arvo konfiguraatio vai salaisuus?
- Mitkä DynamoDB access patternit muutos tarvitsee?
- Onko käsittely idempotentti ja miten virheestä toivutaan?
- Mitä lokeja, metriikoita ja hälytyksiä tarvitaan?
- Mitä testitasoa muutos vaatii?

Jos johonkin näistä ei voi vastata ilman arvausta ja päätös kuuluu pysähtymislistaan, agentti ei saa jatkaa oletuksella.
