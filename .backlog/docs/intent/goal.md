---
id: doc-001
title: Projektin tavoite
type: other
created_date: '2026-06-06 07:19'
tags:
  - intent
  - goal
---
# Projektin tavoite

## Miksi projekti on olemassa

Projekti on olemassa, jotta suomalaisiin yrityksiin liittyvää sijoittaja- ja yritystietoa voidaan seurata keskitetysti yhdestä palvelusta. Käyttäjän ei tarvitse hakea yritysten perustietoja, markkinadataa, uutisia ja sijoittajakeskusteluja erillisistä lähteistä, vaan järjestelmä kokoaa seurattavien yritysten olennaisen tiedon samaan käyttöliittymään.

Palvelun ydin on seurantalista yrityksistä, joihin liittyvää tietoa järjestelmä kerää, tallentaa ja päivittää. Rekisteröityneet ja autentikoidut käyttäjät voivat tarkastella kerättyä tietoa, ja ylläpitäjä voi hallita seurattavia yrityksiä sekä niiden asetuksia. Tavoitteena on tehdä tiedonkeruusta toistettavaa, jäljitettävää ja automatisoitavaa sen sijaan, että käyttäjät joutuvat tekemään saman työn käsin.

## Tavoiteltu lopputila

Valmiissa järjestelmässä käyttäjä kirjautuu selainkäyttöliittymään ja näkee seurattavat yritykset, niiden perustiedot, markkinadataa, uutisia ja yrityksiin liittyviä keskusteluja. Ylläpitäjä voi lisätä, muokata ja poistaa seurattavia yrityksiä sekä määrittää, mitä tietoa yrityksestä kerätään. Tavallinen käyttäjä voi tarkastella kerättyä tietoa roolinsa sallimissa rajoissa.

Backend tarjoaa API:n, jonka kautta frontend käyttää tallennettua dataa ja käynnistää hyväksytyt käyttötapaukset. Markkinadata haetaan EODHD:stä, keskusteluaineisto Inderes Forumista ja yritysten perustietoja PRH:n YTJ Open Data API v3:sta. Ulkoiset lähteet kapseloidaan adaptereihin, jotta lähdekohtaiset mallit, virheet ja kutsukäytännöt eivät vuoda domainiin tai julkisiin API-sopimuksiin.

Järjestelmä toimii AWS serverless -ympäristössä. Julkinen selainkäyttöliittymä julkaistaan CloudFrontin kautta, HTTP-liikenne kulkee API Gatewayn kautta Lambda-funktioille, tiedot tallennetaan DynamoDB:hen, sisäiset tapahtumat ja ajastukset hoidetaan EventBridgellä, konfiguraatio säilytetään Parameter Storessa ja salaisuudet Secrets Managerissa. Backend toteutetaan Python/FastAPI-pohjaisena ports and adapters -arkkitehtuurina, frontend React/Vite/Tailwind/shadcn-pohjaisena SPA-sovelluksena ja API-autentikointi JWT bearer -tokenien avulla.

Tiedonkeruu voidaan ajastaa, jotta yrityksiin liittyvät keskustelut ja markkinadata pysyvät ajan tasalla ilman manuaalista käynnistystä. Auth-, notifications-, marketdata-, comments- ja scheduling-kyvykkyydet muodostavat yhdessä kokonaisuuden, jossa käyttäjähallinta, viestit, tiedonkeruu, keskustelujen synkronointi ja ajastettu tausta-ajo tukevat samaa käyttötarkoitusta.

## Rajaukset

Projekti ei tuota sijoitusneuvontaa, osto- tai myyntisuosituksia, automaattisia kaupankäyntipäätöksiä eikä kaupankäyntitoiminnallisuutta. Järjestelmä kokoaa ja esittää tietoa, mutta vastuu tiedon tulkinnasta jää käyttäjälle.

Projekti ei ole yleinen CRM-, taloushallinto-, analytiikka- tai yritysrekisterijärjestelmä. Yritystiedot mallinnetaan vain siinä laajuudessa kuin seurattavien yritysten hallinta, markkinadata, keskusteluaineisto ja niihin liittyvät käyttötapaukset vaativat.

Keskustelukeruu ei ole yleinen sosiaalisen median keräin. Alkuvaiheen keskusteluaineisto rajataan hyväksyttyihin lähteisiin, erityisesti Inderes Forumiin, ja tuotantokäyttö edellyttää lähteiden käyttöehtojen, robots-käytäntöjen ja lisenssiehtojen tarkistamista. Sama koskee EODHD:n ja YTJ:n käyttöehtoja, lisenssejä ja lähdemainintavaatimuksia.

Alkuvaiheessa järjestelmä ei tavoittele reaaliaikaista streaming-markkinadataa. Markkina- ja keskustelutiedot kerätään käyttötapausten ja ajastusten määrittämällä tavalla, ja mahdollinen reaaliaikaisempi päivitysmalli edellyttää erillistä päätöstä.

Domainia ei sidota AWS:n, HTTP:n, DynamoDB:n, FastAPI:n, Pydanticin, JWT-kirjaston tai ulkoisten API:en malleihin. Teknologiakohtaiset yksityiskohdat kuuluvat adaptereihin, composition rooteihin ja infrastruktuurikerrokseen hyväksyttyjen arkkitehtuuripäätösten mukaisesti.
