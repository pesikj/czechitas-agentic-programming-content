---
id: nasazeni
title: Nasazení
---

# Nasazení: aplikace na internetu

CRM funguje, běží v Dockeru a hlídají ho testy. Teď ho dostaneš tam, kde ho obchodníci Webovky otevřou z vlastního počítače.

## Co je nasazení

> **Kdy se to hodí:** Tři obchodníci Webovky chtějí CRM používat každý ze svého notebooku, v kanceláři i u zákazníka. Na tvém počítači jim to nepomůže: když ho vypneš, CRM zmizí, a data by měl každý jen ve svém.

*Nasazení* (anglicky *deployment*) znamená spustit aplikaci na *serveru*: počítači, který běží nepřetržitě, je připojený k internetu a má veřejnou adresu. Kdo adresu zná, otevře aplikaci v prohlížeči odkudkoli. Všichni pracují se stejnou aplikací a stejnou databází.

Server si můžeš pronajmout a o všechno se starat sám(a): systém, aktualizace, Docker, databázi, zálohy. Jednodušší je *PaaS* (z anglického *Platform as a Service*): služba, které dáš kód a ona se postará o zbytek. Je to rozdíl mezi stavbou domu a pronájmem bytu se službami. V bytě nemusíš řešit střechu ani kotel, jen si přineseš nábytek.

[Railway](https://railway.com) je PaaS, který se hodí přesně pro naše CRM:

- Připojí se k repozitáři na GitHubu. Najde v něm `Dockerfile` z lekce 06 a podle něj postaví obraz aplikace.
- Jedním kliknutím přidá databázi PostgreSQL, stejnou, jakou máš v Dockeru.
- Přidělí aplikaci veřejnou adresu se zabezpečeným připojením (`https://...up.railway.app`).
- Po každém pushi do `main` aplikaci sám znovu nasadí.

Podobně fungují i jiné služby, třeba [Render](https://render.com) nebo [Fly.io](https://fly.io). Postup, který se naučíš, se dá přenést i na ně.

## Vývojové a produkční nastavení

> **Kdy se to hodí:** Nasadíš CRM tak, jak je. Když v aplikaci nastane chyba, Django ukáže žlutou stránku s celým kódem, nastavením a částí hesel. Kdokoli na internetu, kdo chybu vyvolá, ji uvidí taky.

Zatím jsi CRM spouštěl(a) ve *vývojovém* nastavení: pro tebe, na tvém počítači, s podrobnými chybami. Na internetu běží v *produkčním* nastavení, kde ji používají skuteční lidé se skutečnými daty a kde se k ní dostane i kdokoli jiný. Tady je, co se musí změnit:

| Co | Vývoj (u tebe) | Produkce (na Railway) | Proč |
|---|---|---|---|
| `DEBUG` | `True` | `False` | ladicí stránky s kódem a nastavením nesmí vidět cizí lidé |
| `SECRET_KEY` | klidně v kódu | jen v proměnné prostředí | tajný klíč, kterým Django podepisuje přihlášení; kdo ho zná, může se vydávat za uživatele |
| `ALLOWED_HOSTS`, `CSRF_TRUSTED_ORIGINS` | `127.0.0.1` | adresa na Railway | Django odpoví jen na adresy, které zná, a jen z nich přijme formuláře |
| Webový server | `runserver` | *gunicorn* | `runserver` je jen pro vývoj, gunicorn zvládne víc lidí najednou |
| Statické soubory (CSS, obrázky) | servíruje `runserver` | balíček *WhiteNoise* | gunicorn je sám neservíruje |
| Připojení k databázi | `.env` z lekce 06 | proměnná `DATABASE_URL` od Railway | databázi teď spravuje Railway |
| Migrace | spouštíš ručně | příkaz před každým nasazením | databáze musí odpovídat modelům dřív, než aplikace naběhne |

*Proměnné prostředí* znáš z lekce 06: hodnoty, které aplikace dostane zvenku, a ne z kódu. Díky nim je stejný kód v Gitu u tebe vývojový a na Railway produkční.

### Přihlašování

CRM zatím nemá přihlašování. Na tvém počítači to nevadilo. Na internetu by ale kdokoli, kdo zná adresu, viděl všechny zákazníky Webovky a mohl je měnit nebo mazat. **Aplikace s daty zákazníků nesmí být na internetu bez přihlášení.**

Django má přihlašování zabudované. Stačí ho zapnout: všechny stránky budou vyžadovat přihlášení a kdo není přihlášený, uvidí přihlašovací formulář. Účty spravuješ v administraci Djanga, kterou znáš z lekce 06.

Na Railway se ale nemůžeš přihlásit do terminálu kontejneru a spustit `createsuperuser`, jako jsi to dělal(a) v Dockeru. Proto necháš agenta připravit příkaz, který při nasazení vytvoří prvního uživatele z proměnných prostředí, pokud ještě neexistuje.

## Příprava aplikace s agentem

Všechny změny z tabulky necháš udělat agenta. Postupuj stejně jako v minulých lekcích:

1. Udělej commit všech změn a vytvoř větev `nasazeni`.
2. Spusť agenta a pošli mu zadání.

Prompt pro agenta:

```text
Použij skill brainstorming. Chci nasadit tuhle Django aplikaci na Railway.
Railway ji postaví z Dockerfile a dodá databázi PostgreSQL v proměnné
DATABASE_URL a veřejnou adresu v proměnné RAILWAY_PUBLIC_DOMAIN.

Připrav aplikaci na produkci:
- DEBUG a SECRET_KEY ber z proměnných prostředí, výchozí DEBUG je False.
- ALLOWED_HOSTS a CSRF_TRUSTED_ORIGINS nastav podle RAILWAY_PUBLIC_DOMAIN.
- Když existuje DATABASE_URL, připoj se podle ní, jinak použij současné
  nastavení z .env, aby lokální Docker fungoval dál.
- Spouštěj aplikaci přes gunicorn na portu z proměnné PORT.
- Statické soubory servíruj přes WhiteNoise.
- Všechny stránky kromě přihlášení budou vyžadovat přihlášení
  (použij přihlašování, které má Django zabudované).
- Přidej příkaz, který vytvoří správce z proměnných DJANGO_SUPERUSER_USERNAME,
  DJANGO_SUPERUSER_EMAIL a DJANGO_SUPERUSER_PASSWORD, pokud ještě neexistuje.
- Napiš mi, jaký příkaz mám na Railway nastavit, aby se před každým
  nasazením provedly migrace a vytvořil se správce.

Testy musí dál procházet. Přidej test, že nepřihlášený uživatel seznam
firem neuvidí. Kód piš co nejjednodušší a u každé změny vysvětli proč.
```

Zkontroluj v plánu hlavně tři věci. **Žádné heslo ani tajný klíč nesmí být v kódu**, jen názvy proměnných. **Lokální Docker musí fungovat dál**: aplikaci budeš dál vyvíjet u sebe. A **testy**: kromě nového testu přihlášení se budou muset upravit i starší integrační testy, protože stránky teď vyžadují přihlášení. Zkontroluj, že je agent upravil tak, aby se testovací klient nejdřív přihlásil, a ne tak, že by test přestal kontrolovat to, co kontroloval předtím.

Po provedení plánu ověř u sebe:

1. Testy: `docker compose exec web uv run python manage.py test` musí skončit `OK`.
2. Aplikace: `docker compose up --build`, otevři http://127.0.0.1:8000/. Musí se ukázat přihlašovací formulář.

Pak vytvoř pull request, projdi změny a sluč ho do `main`. Railway bude nasazovat právě větev `main`.

## Nasazení na Railway

### 1. Projekt z repozitáře

1. Na [railway.com](https://railway.com) klikni na **New Project** (nebo otevři [railway.com/new](https://railway.com/new)).
2. Vyber **Deploy from GitHub repo**.
3. Pokud tvůj repozitář `crm` v seznamu není, klikni na **Configure GitHub App** a povol Railway přístup k repozitáři `crm`. Railway uvidí jen repozitáře, které mu povolíš.
4. Vyber repozitář `crm`.

Na plátně projektu se objeví *služba* (anglicky *service*) s názvem repozitáře a Railway začne stavět obraz. První nasazení nejspíš selže, protože aplikace zatím nemá databázi ani proměnné. To je v pořádku.

### 2. Databáze

Na plátně projektu klikni na **Create** (nebo pravým tlačítkem do prázdného místa) a vyber **Database → Add PostgreSQL**. Vedle aplikace se objeví druhá služba **Postgres**. Railway pro ni sám vymyslí uživatele a heslo a uloží je do jejích proměnných, mimo jiné do `DATABASE_URL`.

Je to stejné rozdělení jako `web` a `db` v Docker Compose z lekce 06, jen o databázi se teď stará Railway.

### 3. Proměnné prostředí

Klikni na službu s aplikací a otevři záložku **Variables**. Přes **New Variable** přidej:

| Proměnná | Hodnota |
|---|---|
| `DATABASE_URL` | `${{Postgres.DATABASE_URL}}` |
| `SECRET_KEY` | dlouhý náhodný text (vygeneruj si ho, viz níže) |
| `DEBUG` | `False` |
| `DJANGO_SUPERUSER_USERNAME` | tvoje uživatelské jméno |
| `DJANGO_SUPERUSER_EMAIL` | tvůj e-mail |
| `DJANGO_SUPERUSER_PASSWORD` | silné heslo, které nepoužíváš jinde |

Zápis `${{Postgres.DATABASE_URL}}` je *odkaz na proměnnou* jiné služby: Railway do něj dosadí adresu databáze ze služby Postgres. Kdyby se heslo k databázi změnilo, odkaz se aktualizuje sám. Názvy proměnných musí odpovídat tomu, co použil agent. Pokud ti napsal jiné, použij jeho.

Tajný klíč si vygeneruj v terminálu ve VS Code:

```bash
uv run python -c "import secrets; print(secrets.token_urlsafe(50))"
```

Výstup (tvůj bude jiný):

```text
k3J9xQ2mV8pL0rT6wZ1yB4nC7dF5gH2jK8sA0eR3uI9oP6qW1tY4
```

Klíč zkopíruj do proměnné `SECRET_KEY`, nikam jinam ho neukládej a nikomu neposílej.

### 4. Migrace a správce před nasazením

Otevři záložku **Settings** služby s aplikací a najdi pole pro *pre-deploy command*: příkaz, který Railway spustí před každým nasazením, v samostatném kontejneru. Když skončí chybou, nové nasazení se nespustí a dál běží předchozí verze. Proto se do něj hodí migrace: aplikace nikdy nenaběhne nad databází, která neodpovídá modelům.

Vlož do pole příkaz, který ti napsal agent. Bude vypadat podobně jako:

```text
uv run python manage.py migrate && uv run python manage.py vytvor_spravce
```

### 5. Veřejná adresa

V **Settings** v části **Networking** klikni na **Generate Domain**. Pokud se Railway zeptá na port, zadej ten, na kterém aplikace podle logů poslouchá (najdeš ho v řádku od gunicornu `Listening at: http://0.0.0.0:...`). Railway přidělí adresu ve tvaru `crm-production-xxxx.up.railway.app`.

### 6. Nasaď

Railway změny v proměnných a nastavení nejdřív jen připraví. Nahoře na plátně se objeví tlačítko **Deploy**, kterým je použiješ. Klikni na něj a sleduj nasazení v záložce **Deployments**.

Když nasazení doběhne, otevři vygenerovanou adresu. Uvidíš přihlašovací formulář. Přihlas se jménem a heslem z proměnných, přidej firmu a obchodní případ. Pak adresu otevři i na telefonu: CRM teď běží na internetu.

### Automatické nasazení

Od teď Railway nasadí novou verzi po každém pushi do `main`. Proto se vyplatí postup z lekce 04: změny dělej ve větvi, projdi je v pull requestu, spusť testy a teprve pak sluč do `main`. Co se dostane do `main`, je za pár minut na internetu.

## Když se něco pokazí

Nasazení selže častěji, než bys čekal(a), hlavně napoprvé. Klikni v záložce **Deployments** na nasazení a otevři **View logs**. Railway ukazuje dva druhy logů:

- **Build Logs** – stavění obrazu podle `Dockerfile`. Na začátku uvidíš `Using detected Dockerfile!`. Chyba tady znamená, že se obraz nepostavil, třeba chybí balíček.
- **Deploy Logs** – běh aplikace: pre-deploy příkaz, start gunicornu a každý požadavek. Chyba tady znamená, že obraz je v pořádku, ale aplikace nenaběhla nebo padá.

Logy čteš stejně jako v lekci 03: hledej `ERROR` a traceback a čti odspodu. Nejčastější problémy:

| Co vidíš | Co to nejspíš znamená |
|---|---|
| `DisallowedHost` v logu, v prohlížeči chyba 400 | adresa z Railway není v `ALLOWED_HOSTS` |
| `CSRF verification failed` po odeslání formuláře | adresa není v `CSRF_TRUSTED_ORIGINS` |
| `Application failed to respond` | aplikace neposlouchá na portu z proměnné `PORT` |
| stránka bez stylů, administrace vypadá rozbitě | nefungují statické soubory (WhiteNoise) |
| `relation "obchod_firma" does not exist` | neproběhly migrace, zkontroluj pre-deploy příkaz |

Když si nevíš rady, zkopíruj z logu traceback a pošli ho agentovi spolu s tím, co jsi dělal(a). Opravu udělej ve větvi, otestuj u sebe a dostaň ji do `main` přes pull request.

**Návrat k funkční verzi.** Když nová verze nefunguje a obchodníci potřebují CRM hned, vrať se k předchozí: v záložce **Deployments** klikni u starší funkční verze na tři tečky a vyber **Rollback**. Railway vrátí obraz i proměnné té verze. Chybu pak opravíš v klidu. Ve zkušebním období uchovává Railway starší obrazy jen 24 hodin, potom se k nim vrátit nedá.

## Cena a úklid

Railway účtuje podle toho, kolik aplikace a databáze spotřebují paměti, výkonu procesoru a místa na disku, i když je zrovna nikdo nepoužívá. Malé CRM spotřebuje za měsíc jednotky dolarů. Kolik už stálo, uvidíš v přehledu **Usage** ve svém účtu.

Zkušební kredit 5 USD platí 30 dní. Pak účet přejde na bezplatný plán s kreditem 1 USD měsíčně, který na nepřetržitý běh aplikace s databází nestačí. Data v databázi Railway smaže 30 dní po vypršení kreditu.

Až aplikaci nebudeš potřebovat, smaž celý projekt: **Settings** projektu → **Danger** → smazání projektu. Tím zmizí aplikace i databáze. Data, která chceš zachovat, si předtím zálohuj.

## Cvičení: CRM na internetu

Nasaď CRM na Railway a ověř, že funguje bezpečně.

1. **Příprava.** Ve větvi `nasazeni` nech agenta připravit aplikaci podle promptu výše. Ověř testy a přihlašování u sebe a dostaň změny přes pull request do `main`.
2. **Nasazení.** Vytvoř na Railway projekt z repozitáře, přidej PostgreSQL, nastav proměnné, pre-deploy příkaz a veřejnou adresu a nasaď.
3. **Bezpečnost.** Otevři adresu v anonymním okně prohlížeče. Vidíš seznam firem, nebo přihlašovací formulář? Zkus otevřít neexistující stránku (třeba `/neexistuje/`). Vidíš žlutou ladicí stránku Djanga, nebo obyčejnou chybu 404?
4. **Automatické nasazení.** Ve větvi změň nadpis stránky se seznamem firem, sluč změnu do `main` a sleduj, jak ji Railway nasadí.
5. **Rollback.** Vrať se na Railway k předchozímu nasazení a ověř, že je nadpis zase původní. Pak se vrať k nejnovějšímu.

```exercise
id: crm-railway
revision: 1
title: CRM na internetu
fields:
  - id: adresa
    label: Adresa aplikace
    guidance: Na jaké adrese CRM běží? Přihlásil(a) ses?
  - id: problemy
    label: Co se při nasazení pokazilo
    guidance: Které nasazení selhalo a proč? Našel(a) jsi chybu v Build Logs, nebo v Deploy Logs? Jak jsi ji opravil(a)?
  - id: bezpecnost
    label: Bezpečnost
    guidance: Co jsi viděl(a) v anonymním okně? Ukázala se u neexistující stránky ladicí stránka Djanga? Jsou v repozitáři nějaká hesla?
  - id: testy
    label: Úprava testů
    guidance: Jak agent upravil starší integrační testy kvůli přihlašování? Kontrolují pořád to, co předtím?
  - id: rollback
    label: Automatické nasazení a rollback
    guidance: Jak dlouho trvalo, než se změna z main objevila na internetu? Fungoval rollback?
```

## Cvičení: Nasazení vlastního projektu

U vlastního projektu si nejdřív ujasni, co nasazení znamená pro tvoje uživatele a jejich data.

1. **Kdo k aplikaci smí.** Rozhodni, jestli aplikace potřebuje přihlášení, a pokud ano, kdo bude mít účet. Uvažuj podle dat: obsahuje aplikace osobní údaje, například jména, telefony nebo zdravotní informace?
2. **Co se změní.** Projdi tabulku vývojového a produkčního nastavení a u každého řádku zapiš, jestli se týká i tvé aplikace. Zapiš to do `produkt.md` do nové sekce "Nasazení".
3. **Nasaď.** Pokud už tvoje aplikace běží v Dockeru, připrav ji s agentem stejně jako CRM a nasaď ji na Railway jako druhý projekt. Hlídej spotřebu: dvě aplikace s databází spotřebují kredit rychleji.

```exercise
id: vlastni-projekt-nasazeni
revision: 1
title: Nasazení vlastního projektu
fields:
  - id: pristup
    label: Kdo k aplikaci smí
    guidance: Potřebuje aplikace přihlášení? Jaká data v ní budou a kdo by je neměl vidět?
  - id: zmeny
    label: Co se pro produkci musí změnit
    guidance: Které řádky tabulky se týkají tvé aplikace? Je tam něco navíc, co CRM nepotřebovalo?
  - id: adresa
    label: Adresa nasazené aplikace
    guidance: Pokud jsi aplikaci nasadil(a), na jaké adrese běží? Co se při nasazení pokazilo?
```
