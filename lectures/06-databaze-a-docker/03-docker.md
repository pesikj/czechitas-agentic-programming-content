---
id: docker
title: Docker
---

# Docker: aplikace, která běží všude stejně

Teď už víš, kde CRM ukládá data. Zatím ale všechno běží jen na tvém počítači: tvůj Python, tvoje balíčky, tvůj soubor `db.sqlite3`. Než aplikaci později v kurzu nasadíš na internet, potřebuješ ji zabalit tak, aby fungovala kdekoli. K tomu slouží Docker.

## Problém "u mě to funguje"

> **Kdy se to hodí:** Pošleš CRM kolegyni. Ta má jinou verzi Pythonu, na Windows se jí nespustí jeden příkaz a databázi má prázdnou. Hodinu hledáte rozdíly mezi vašimi počítači, místo abyste pracovaly na aplikaci.

Aplikace nikdy neběží sama. Potřebuje operační systém, správnou verzi Pythonu, balíčky a databázi. Na každém počítači je tohle okolí trochu jiné, a proto aplikace, která "u mě funguje", jinde spadne.

## Co je Docker

*Docker* zabalí aplikaci i s celým okolím, které potřebuje, do jednoho balíku. Ten pak běží všude stejně: na Windows, na macOS i na serveru.

Funguje to jako lodní kontejner. Než se kontejnery zavedly, nakládal se každý náklad jinak: pytle, sudy, bedny. Kontejner má standardní rozměry, takže ho přenese jakákoli loď, jeřáb nebo kamion, a nikoho nezajímá, co je uvnitř.

Tři pojmy, které budeš potkávat:

- *Obraz* (anglicky *image*) je zabalená aplikace i s okolím: systém, Python, balíčky, kód. Je to jako šablona, ze které se nic nemění.
- *Kontejner* (anglicky *container*) je spuštěný obraz. Z jednoho obrazu můžeš spustit víc kontejnerů.
- *Dockerfile* je textový soubor s receptem, jak obraz postavit: "vezmi Python, nainstaluj uv, zkopíruj kód, nainstaluj balíčky".

Hotové obrazy si můžeš stáhnout z katalogu [Docker Hub](https://hub.docker.com), podobně jako balíčky z PyPI. Je tam třeba oficiální obraz databáze PostgreSQL.

Docker Desktop sis nainstaloval(a) v lekci 01. Spusť ho, počkej, až se rozběhne, a v terminálu ve VS Code ověř:

```bash
docker version
```

Výstup musí obsahovat část **Client** i **Server**. Pokud chybí Server, Docker Desktop ještě neběží.

## Docker Compose: víc kontejnerů najednou

Pravidlo Dockeru je *jeden kontejner, jedna věc*. CRM proto rozdělíš na dvě části:

- **web** – aplikace v Djangu,
- **db** – databáze.

*Docker Compose* je nástroj, který spustí a propojí víc kontejnerů najednou. Popíšeš je v souboru `compose.yaml`: jaké kontejnery chceš, z jakých obrazů a jak spolu mluví. Pak celou aplikaci spustíš jedním příkazem.

**Proč samostatná databáze?** SQLite je soubor, se kterým pracuje přímo aplikace. Na jednom počítači to stačí. Na serveru, kde CRM používá víc obchodníků najednou, se používá databázový server, třeba *PostgreSQL*. Běží jako samostatný program, zvládne mnoho uživatelů současně a dá se zálohovat a spravovat odděleně od aplikace. Django s ním umí pracovat stejně jako se SQLite: modely i migrace zůstanou stejné, změní se jen nastavení připojení.

Data databáze v kontejneru se ukládají do *volume* (svazek): úložiště, které Docker spravuje mimo kontejner. Kontejner můžeš smazat a znovu vytvořit a data zůstanou.

## Převod CRM na Docker Compose

Převod je větší změna, která se dotkne nastavení, nových souborů i databáze. Postupuj stejně jako v minulé lekci:

1. Udělej commit všech změn a vytvoř větev `docker` (lekce 04). Když se převod nepovede, vrátíš se do `main`.
2. Zazálohuj `db.sqlite3`.
3. Spusť agenta a pošli mu zadání. Agent s ním projde brainstorming a ze schváleného návrhu napíše plán.

Prompt pro agenta:

```text
Převeď tuhle Django aplikaci tak, aby běžela v Dockeru pomocí Docker Compose.
Chci dva kontejnery:
- web: Django aplikace. Obraz postav z Dockerfile, balíčky instaluj přes uv
  podle pyproject.toml a uv.lock.
- db: databáze PostgreSQL z oficiálního obrazu postgres. Data ukládej do
  pojmenovaného volume, aby po restartu nezmizela.

Django se k databázi připojí přes proměnné prostředí (název databáze,
uživatel, heslo, adresa). Hesla dej do souboru .env, který nebude v Gitu,
a vytvoř vzorový soubor .env.example s vymyšlenými hodnotami.
Při spuštění kontejneru web se provedou migrace.
Popiš i, jak přenesu data, která už mám v SQLite.

Kód piš co nejjednodušší a u každého nového souboru vysvětli, k čemu slouží.
Použij skill brainstorming a ze schváleného návrhu pak napiš plán.
U každého úkolu napiš, jak ověřím, že funguje.
```

Zadání říká, *kolik* kontejnerů chceš a *co* v nich poběží, *kde* mají zůstat data a *jak* zacházet s hesly. Bez poslední části by agent hesla klidně napsal přímo do `compose.yaml`, a ten se uloží do Gitu.

## Co v plánu hledat

Plán se bude lišit, ale měl by obsahovat tyhle soubory a změny. Když něco chybí, zeptej se agenta proč:

| Soubor | K čemu slouží |
|---|---|
| `Dockerfile` | recept na obraz aplikace: Python, uv, balíčky, kód |
| `compose.yaml` | popis kontejnerů `web` a `db`, jejich propojení a volume pro data |
| `.env` | skutečná hesla a nastavení, jen na tvém počítači, v `.gitignore` |
| `.env.example` | vzor `.env` s vymyšlenými hodnotami, ten do Gitu patří |
| `.dockerignore` | co nekopírovat do obrazu, třeba `.venv` nebo `db.sqlite3` |
| `config/settings.py` | připojení k databázi z proměnných prostředí místo SQLite |
| `pyproject.toml` | nový balíček pro připojení k PostgreSQL (obvykle `psycopg`) |

Zkontroluj hlavně dvě věci. **Hesla** nesmějí být v souborech, které jdou do Gitu. **Přenos dat**: databáze v kontejneru začne prázdná. Data ze SQLite se obvykle přenášejí tak, že je Django vypíše do souboru příkazem `dumpdata` a v novém kontejneru je načte příkazem `loaddata`. Pokud plán přenos dat neřeší, firmy z minulé lekce v nové databázi nebudou.

Plán schval a nech ho provést stejně jako v minulé lekci. Když agent nabídne worktree, odmítni: pracuješ ve větvi `docker`.

## Spuštění a ověření

Celou aplikaci spustíš v terminálu ve VS Code:

```bash
docker compose up --build
```

`--build` znamená, že Docker nejdřív podle `Dockerfile` postaví obraz aplikace. Poprvé to trvá několik minut, protože stahuje Python i PostgreSQL. V terminálu pak běží výpis obou kontejnerů. Otevři http://127.0.0.1:8000/ a ověř, že CRM funguje.

V druhém terminálu se podívej, které kontejnery běží:

```bash
docker compose ps
```

Měl(a) bys vidět dva řádky, `web` a `db`. Uvidíš je i v Docker Desktopu v části **Containers**.

Příkazy Djanga teď spouštíš uvnitř kontejneru `web` přes `docker compose exec`. Přesný tvar ti ukáže agent, obvykle třeba takhle vytvoříš uživatele pro administraci:

```bash
docker compose exec web uv run python manage.py createsuperuser
```

Aplikaci zastavíš klávesami `Ctrl C` v terminálu, kde běží, a kontejnery odstraníš příkazem `docker compose down`. Data ve volume zůstanou. Pozor na `docker compose down -v`: přepínač `-v` smaže i volume, tedy celou databázi.

**Ověř, že data přežijí restart.** Přidej firmu, spusť `docker compose down` a pak znovu `docker compose up`. Firma musí v seznamu zůstat.

## Cvičení: CRM v Dockeru

Převeď s agentem CRM na Docker Compose podle postupu výše, ve větvi `docker`. Přenes do nové databáze firmy a obchodní případy ze SQLite. Ověř, že aplikace běží, že data přežijí `docker compose down` a nové spuštění a že v Gitu nejsou hesla. Nakonec větev pošli na GitHub a přes pull request ji sluč do `main`.

```exercise
id: crm-v-dockeru
revision: 1
title: CRM v Dockeru
fields:
  - id: soubory
    label: Nové soubory a jejich účel
    guidance: Které soubory agent vytvořil nebo změnil? Uměl(a) bys vysvětlit, k čemu každý slouží?
  - id: hesla
    label: Kde jsou hesla
    guidance: Ve kterém souboru jsou hesla k databázi? Jak jsi ověřil(a), že nejsou v Gitu?
  - id: data
    label: Přenos a trvanlivost dat
    guidance: Jak jsi přenesl(a) data ze SQLite? Zůstala po down a novém up?
```
