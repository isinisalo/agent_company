---
id: roadmap-001
title: Release roadmap
created_date: '2026-06-07 18:08'
status: accepted
type: decision
tags:
  - roadmap
  - release
  - milestones
---
# Milestones

## M0 Specification readiness

### Objective

Valmistele agenttien toteutustyö niin, että projektin pysyvät rajat, context-kohtaiset sopimukset ja validointitavat ovat yksiselitteiset ennen varsinaista tuotetoteutusta.

### Required outcomes

- Määritä repo-rakenne ja kapeimmat laatukomennot alueille `backend/`, `frontend/` ja `infra/` ilman uusia top-level sovellushakemistoja.
- Määritä API boundary -konventiot: versiointi, principal, JWT bearer -raja, virhevastaukset, CORS-vaikutukset ja raw-mallien vuotamattomuus.
- Määritä bounded context -kartta ja sanasto contexteille Auth, Notifications, Companies/watchlist, Marketdata, Comments ja Scheduling.
- Määritä context-kohtaiset detail-spesifikaatiot vain toteutuksen tarvitsemalle domain-, API- ja persistence-tasolle.
- Määritä poikkileikkaavat security-, data-, config-, secrets-, operations- ja external-source-compliance-guardrailit.

### Exit gate

M0 on valmis, kun agentti voi aloittaa toteutustehtävän ilman, että sen tarvitsee lukita julkista API:a, DynamoDB key/index -mallia, IAM-scopea, retentionia, deletion-sääntöä tai tuotantolähteen compliance-rajaa ilman hyväksyttyä spesifikaatiota. Pysähdy, jos jokin näistä sopimuksista puuttuu ja toteutus vaatisi pysyvän päätöksen.

## M1 Walking skeleton

### Objective

Toteuta hyväksyttyyn arkkitehtuuriin sopiva ohut päästä päähän -runko, joka todistaa selainkäyttöliittymän, API:n, backendin, infran ja mock-only-lähteiden yhteensopivuuden.

### Required outcomes

- Luo monorepon sovellusrunko hyväksytyille alueille `backend/`, `frontend/` ja `infra/`.
- Lisää GitHub Actions -laatuportit vähintään aluekohtaisille tarkistuksille, jotka on määritetty M0:ssa.
- Toteuta minimaalinen Python 3.14 FastAPI + Mangum Lambda -polku API Gatewayn ja AWS SAM -templaten kautta.
- Toteuta React TypeScript Vite SPA -käyttöliittymärunko Tailwind CSS:llä ja shadcn/ui-pohjalla.
- Toteuta JWT bearer -reunan ja eksplisiittisen `Principal`-olion minimitoteutus ilman, että domain käsittelee raakaa tokenia.
- Toteuta DynamoDB-adapterin muoto ja mock-only ulkoisten lähteiden adapterirajat ilman tuotantokutsuja.
- Näytä selaimessa yksi pystysuora virta, jossa seurattava yritys näkyy placeholder-tasoisilla lähdeattribuoiduilla perustieto-, markkinadata-, keskustelu- ja keruutilapaneeleilla.

### Exit gate

M1 on valmis, kun walking skeleton toimii paikallisesti ja CI:ssä ilman oikeita credentialeja, tuotantodataa tai ulkoisten lähteiden tuotantokutsuja. Toteutus ei saa riippua Mockoonista tuotantokoodissa eikä vuodattaa AWS-, HTTP-, DynamoDB-, Pydantic-, JWT- tai provider-raakamalleja domainiin.

## M2 P0 implementation

### Objective

Toteuta tuotteen ensimmäinen varsinainen käyttökokonaisuus: käyttäjä voi kirjautuneena seurata suomalaista yritystä ja nähdä yrityksen koontinäkymässä perustiedot, markkinadatan, keskusteluaineiston ja tiedonkeruun tilan.

### Required outcomes

- Auth tukee rekisteröintiä, kirjautumista, sähköpostivahvistusta, salasanan resetointia ja admin-käyttäjähallinnan P0-virtoja hyväksyttyjen security-rajojen sisällä.
- Notifications tukee viestipyyntöä, hyväksyttyä template-renderöintiä, mock-only-toimitusta ja turvallista toimitustilan kyselyä.
- Companies/watchlist tukee seurattavan yrityksen lisäämistä, päivittämistä, poistamisen rajattua käsittelyä, listausta ja mock-only YTJ-perustietopäivitystä.
- Marketdata tukee seurattavan yrityksen mock-only EODHD-haun, normalisoinnin, tallennuksen, lähdeattribuution ja rajatun summaryn näyttämisen.
- Comments tukee yrityksen hyväksyttyyn Inderes Forum -topicciin perustuvaa mock-only-hakua, normalisointia, deduplikointia, cursorin tallennusta ja rajattua näyttämistä.
- Scheduling tukee keruuajastuksen määrittämistä, erääntyneen ajon idempotenttia käynnistystä, tuloksen tallennusta, retryä, failed-tilaa ja compliance-puutteisen tuotantokeruun estoa.
- Yrityksen koontinäkymä näyttää perustiedot, markkinadatasummaryn, topic-perusteiset kommentit, lähteen, hakuajankohdan ja keruutilan käyttäjän oikeuksien mukaisesti.

### Exit gate

M2 on valmis, kun P0-virrat toimivat mock-only-lähteillä ilman salaisuuksien, credentialien, tokenien, password hashien, PII:n, tokenillisten URL:ien tai providerin raw-virheiden vuotoa. EODHD, PRH:n YTJ Open Data API v3 ja Inderes Forum ovat hyväksytyt lähteet, mutta tuotantokäyttö pysyy estettynä ilman erillistä compliance-evidenssiä ja käyttäjän hyväksyntää.

## M3 Edge cases and quality

### Objective

Koveta P0-toteutus virhe-, reuna-, idempotenssi-, authorization- ja käyttöliittymätilanteisiin niin, että release-kandidaatti ei perustu vain onnistuneisiin happy path -virtoihin.

### Required outcomes

- Testaa ja korjaa validointivirheet, authorization-hylkäykset, käyttäjän enumeration-riskit, duplikaattiyritykset, puuttuvat topicit, puuttuvat keruuasetukset ja seurannasta poistetut yritykset.
- Varmista idempotentti keruu, retry-rajat, failed-tilat, cursorin päivitys, deduplikointi, sivutus, tyhjät tilat ja turvalliset lähdevirheluokat.
- Varmista, ettei EODHD-, YTJ- tai Inderes-raw-malli vuoda domainiin, julkiseen API:in, fixtureihin tai lokiin.
- Toteuta kohdennetut domain/use case -yksikkötestit, adapteritestit moto 5- ja responses-mockeilla sekä Playwright Given/When/Then -testit korkean arvon selainvirroille Page Object -mallilla.
- Varmista frontendin ESLint-, Jest- ja Playwright-polut sekä backendin Ruff-, mypy- ja testipolut M0:ssa määritellyillä komennoilla.

### Exit gate

M3 on valmis, kun acceptance-kriittiset onnistumis-, hylkäys-, idempotenssi-, authorization-, lähdevirhe-, tyhjätila- ja no-secret/no-PII-skenaariot on testattu tai eksplisiittisesti rajattu release-riskiksi. Sama käyttäytyminen ei saa olla tarpeettomasti päällekkäin useassa testitasossa.

## M4 Security and operations

### Objective

Viimeistele releaseä estävät security-, operointi-, compliance- ja deployment-rajat ennen tuotantoon vietävää päätöstä.

### Required outcomes

- Viimeistele secrets- ja config-katalogi Parameter Storelle, Secrets Managerille ja hyväksytyille ei-salaisille base URL -avaimille.
- Varmista lokituksen redaktio ja kielto lokittaa credentialeja, API-avaimia, JWT:itä, token-digestejä, salasanoja, password hasheja, tarpeetonta PII:tä, raw-lähdevirheitä tai tokenillisia URL:eja.
- Rajaa IAM-oikeudet vähimpään tarpeeseen ja dokumentoi stop-sääntö uusille AWS-palveluille, laajoille wildcard-oikeuksille ja pysyville konsolimuutoksille.
- Viimeistele SAM-, EventBridge-, API Gateway-, CloudFront- ja CORS-rajat hyväksytyn AWS serverless -mallin sisällä.
- Dokumentoi retention-, deletion-, deploy-, rollback-, smoke-test- ja operointirunbookit.
- Dokumentoi tuotantolähteiden ehdot, kutsurajat, aikakatkaisut, retry-rajat, credential-käsittely, retention, PII-käsittely, lokitusrajat ja evidenssi ennen yhtään live-keruuta.

### Exit gate

M4 on valmis, kun tuotantokeruu pysyy teknisesti ja prosessillisesti estettynä kaikilta lähteiltä, joilta puuttuu hyväksytty credential-käsittely, käyttöehdot, kutsurajat, retention, PII-käsittely, operointiraja tai käyttäjän hyväksyntä. Tuotantodeploy, tuotantodata, cloud-oikeudet ja live external-source -käyttö vaativat eksplisiittisen hyväksynnän.

## M5 Release

### Objective

Julkaise release-kandidaatti vain, kun tuotteen hyväksytty P0-arvo on todennettu, stop-säännöt toimivat ja jäljellä olevat rajaukset ovat näkyviä.

### Required outcomes

- Aja CI ja kaikki releaseen kuuluvat backend-, frontend-, infra- ja selainvalidoinnit.
- Varmista, että acceptance-kriteerit täyttyvät Auth-, Notifications-, Companies/watchlist-, Marketdata-, Comments- ja Scheduling-virroille.
- Kirjaa release notes, tunnetut rajaukset, mock-only- tai hyväksytty-live-datakäyttäytyminen ja operointiohjeet.
- Tee staging- tai vastaava smoke check hyväksytyllä ympäristörajalla.
- Varmista, ettei julkaisu sisällä sijoitusneuvontaa, osto- tai myyntisuosituksia, automaattisia kaupankäyntipäätöksiä, kaupankäyntitoiminnallisuutta, yleistä CRM:ää, yleistä yritysrekisteriä tai sosiaalisen median yleiskeräintä.

### Exit gate

M5 on valmis, kun release-kandidaatti voidaan osoittaa toimivaksi selainkäyttöiseksi yritysseurantapalveluksi, jossa seurattava yritys lisätään kerran ja järjestelmä kerää, tallentaa, attribuoi ja näyttää hyväksytyn tiedon ilman manuaalista lähdehakua. Julkaisu ei saa sisältää tuotantodeployta, tuotantodataa tai live-lähdekutsua ilman käyttäjän eksplisiittistä hyväksyntää.
