---
id: chyby-a-logy
title: Chyby, výjimky a balíčky
---

# Chyby, výjimky a balíčky

Víš, co je program, umíš ho spustit v terminálu a víš, jak s tebou spolupracuje agent. Teď si program s nákupem opravdu necháš napsat, spustíš ho – a pak ho schválně rozbiješ. Uvidíš, jak vypadají chyby a jak se před nimi program může chránit. Nakonec do projektu přidáš hotový nástroj od jiných lidí a necháš program pracovat s aktuálním kurzem eura.

Tyhle principy potřebuješ znát, i když kód píše AI. Chyby se objeví vždycky a ty musíš poznat, co se stalo, a posoudit, jestli je oprava od agenta opravdu oprava.

## Data v souboru CSV

> **Kdy se to hodí:** Seznam nákupu nechceš mít natvrdo v kódu. Když přidáš novou položku, chceš upravit jen seznam, ne program.

Ceny z minulé části jsou teď v souboru `nakup.csv`. *CSV* (anglicky *comma-separated values*) je obyčejný textový soubor s tabulkou: každý řádek je jeden řádek tabulky a hodnoty jsou oddělené čárkou. První řádek obsahuje názvy sloupců.

```text
polozka,cena,mena
Batoh,1290,CZK
Spacák,45,EUR
Karimatka,590,CZK
Čelovka,18,EUR
Láhev na vodu,249,CZK
```

Měny jsou zapsané mezinárodními kódy: `CZK` pro koruny a `EUR` pro eura.

Otevři ve VS Code projekt `nakup`, který sis vytvořil(a) na začátku minulé části. Stáhni soubor [nakup.csv](data/nakup.csv) a ulož ho do složky `nakup`. Ve VS Code se objeví v panelu Explorer. Ověř to i v terminálu ve VS Code:

```bash
ls
```

Výpis by měl obsahovat `nakup.csv`. Pokud ho nevidíš, soubor se nejspíš uložil do složky Stažené soubory – přesuň ho do `Documents/nakup`.

Soubor CSV otevírej a upravuj ve Visual Studio Code, ne v Excelu. Excel umí CSV při ukládání nenápadně změnit, třeba nahradit čárky středníky nebo pokazit češtinu.

## Kód od agenta

Spusť agenta v terminálu ve VS Code (příkazem `codex` nebo `claude`) – terminál už je ve složce `nakup`, takže agent bude pracovat v tvém projektu. V desktopové aplikaci vyber jako projekt složku `nakup`.

Prompt pro agenta:

```text
Ve složce je soubor nakup.csv se sloupci polozka, cena a mena (CZK nebo EUR).
Napiš v Pythonu program nakup.py, který sečte všechny ceny v Kč.
Eura převeď kurzem 1 EUR = 25 Kč. Program spustím příkazem uv run nakup.py.
```

Agent může vygenerovat například tento kód. Tvůj se může lišit – důležité je, aby dělal totéž:

```python
import csv

KURZ_EUR = 25


def nacti_polozky(cesta):
    with open(cesta, encoding="utf-8", newline="") as soubor:
        return list(csv.DictReader(soubor))


def cena_v_kc(polozka):
    cena = float(polozka["cena"])
    if polozka["mena"] == "EUR":
        return cena * KURZ_EUR
    return cena


polozky = nacti_polozky("nakup.csv")
celkem = 0
for polozka in polozky:
    celkem += cena_v_kc(polozka)

print(f"Celkem: {celkem:.2f} Kč")
```

Spusť program:

```bash
uv run nakup.py
```

Výstup:

```text
Celkem: 3704.00 Kč
```

Je to stejný výsledek, jaký jsme spočítali ručně v trasovací tabulce. Program je deterministický, takže víme, co má vyjít – a vyšlo to.

### Jak kód číst

Nemusíš umět takový kód napsat. Měl(a) bys ale zhruba poznat, co která část dělá:

- `import csv` – načte nástroj na čtení souborů CSV, který je součástí Pythonu.
- `KURZ_EUR = 25` – proměnná s kurzem. Velká písmena naznačují, že se hodnota během programu nemění.
- `for polozka in polozky:` – *opakování*: pro každou položku ze souboru proveď odsazený řádek pod tím.
- `if polozka["mena"] == "EUR":` – *rozhodování*: jen pokud je měna EUR, vynásob cenu kurzem.
- `float(...)` – převede text ze souboru na číslo. V souboru je totiž všechno text, i `1290`.
- `f"Celkem: {celkem:.2f} Kč"` – text, do kterého se dosadí hodnota proměnné `celkem` zaokrouhlená na dvě desetinná místa.

Opakování a rozhodování znáš z pseudokódu. Nové jsou tu *funkce*.

### Funkce

> **Kdy se to hodí:** Převod ceny na koruny potřebuješ na několika místech programu. Nechceš ho psát pořád znovu – a když se pravidlo změní, chceš ho opravit na jednom místě.

*Funkce* (anglicky *function*) je pojmenovaný kus kódu, který udělá jeden konkrétní úkol. Je to jako recept s názvem: jednou ho sepíšeš a pak už jen řekneš "udělej palačinky".

```python
def cena_v_kc(polozka):
    cena = float(polozka["cena"])
    if polozka["mena"] == "EUR":
        return cena * KURZ_EUR
    return cena
```

- `def` říká, že tady začíná nová funkce s názvem `cena_v_kc`.
- `polozka` v závorce je *parametr* – vstup, se kterým funkce pracuje.
- `return` vrátí výsledek – výstup funkce. Jakmile funkce narazí na `return`, končí.

Funkci použiješ (*zavoláš*) jejím názvem: `cena_v_kc(polozka)`. Program s nákupem má dvě funkce: `nacti_polozky` načte soubor a `cena_v_kc` převede jednu cenu. Každá dělá jednu věc a z názvu je jasné jakou. Díky tomu se v kódu snáz vyznáš ty i agent.

## Syntaktická chyba: program se nespustí

Teď program rozbijeme. Nejdřív si představ, že v posledním řádku chybí uzavírací závorka:

```python
print(f"Celkem: {celkem:.2f} Kč"
```

Po spuštění dostaneš:

```text
  File "/Users/jana/Documents/nakup/nakup.py", line 23
    print(f"Celkem: {celkem:.2f} Kč"
         ^
SyntaxError: '(' was never closed
```

Tohle je *syntaktická chyba* (anglicky *syntax error*): kód porušuje pravidla zápisu jazyka. Python ho proto vůbec nezačne provádět – ani první řádky, které jsou v pořádku. Zpráva ti řekne, ve kterém souboru a na kterém řádku chyba je (`line 23`), šipka `^` ukazuje na místo, kde Python zpozorněl, a poslední řádek popisuje problém: závorka `(` nebyla nikdy uzavřena.

Syntaktické chyby jsou ty příjemnější. Program spadne hned, chybová hláška ukáže přímo na místo a oprava bývá jednoduchá. V kódu od AI se objevují málokdy.

## Chyba za běhu: problém v datech

Vrať závorku zpátky. Teď nebudeš měnit kód, ale data. Otevři `nakup.csv` ve VS Code a u karimatky udělej překlep: místo nuly napiš velké písmeno O.

```text
Karimatka,59O,CZK
```

Takový překlep se snadno stane, když data přepisuješ ručně – a na první pohled ho skoro nevidíš. Spusť program znovu:

```text
Traceback (most recent call last):
  File "/Users/jana/Documents/nakup/nakup.py", line 21, in <module>
    celkem += cena_v_kc(polozka)
              ~~~~~~~~~^^^^^^^^^
  File "/Users/jana/Documents/nakup/nakup.py", line 12, in cena_v_kc
    cena = float(polozka["cena"])
ValueError: could not convert string to float: '59O'
```

Tohle je *chyba za běhu* (anglicky *runtime error*). Kód je zapsaný správně, program se spustil, ale při práci narazil na situaci, se kterou si neporadil: text `59O` nejde převést na číslo. Stejně by dopadl, kdyby cena chyběla úplně (`Karimatka,,CZK`).

Výpisu se říká *traceback* – stopa, kudy program šel, než spadl. Čti ho odspodu:

1. **Poslední řádek** říká, co se stalo: `ValueError`, text `'59O'` nejde převést na číslo.
2. **Nad ním** je místo, kde k chybě došlo: řádek 12 ve funkci `cena_v_kc`.
3. **Ještě výš** je místo, odkud byla funkce zavolaná: řádek 21.

Všimni si, že chyba není v kódu, ale v datech. Program se data zatím nesnažil kontrolovat – předpokládal, že každá cena je číslo. Je to stejný druh problému jako s eury v minulé části: skrytý předpoklad o datech, který přestal platit.

## Oprava s pomocí AI

Požádej agenta o pomoc. Nejlepší je dát mu celý traceback, ne jen poslední řádek.

Prompt pro agenta:

```text
Program nakup.py skončil touto chybou:

<sem vlož celý traceback>

Nejdřív mi vysvětli, co se stalo a kde je příčina. Pak navrhni opravu.
```

Agent může navrhnout dvě různé věci:

- **Opravit data:** v souboru `nakup.csv` změnit `59O` na `590`. To je skutečná oprava příčiny.
- **Upravit kód,** aby s chybnou hodnotou nespadl. To zní rozumně – ale pozor, jak přesně to udělá. O tom je další kapitola.

Oprav nejdřív data a ověř, že program zase vypíše `Celkem: 3704.00 Kč`. Pak vrať překlep zpátky, ať máš na čem zkoušet další úpravy.

## Výjimky: program nespadne, ale...

> **Kdy se to hodí:** Seznam nákupu nevyplňuješ jen ty, ale celá rodina. Nechceš, aby jeden překlep shodil celý program.

V Pythonu se chybě za běhu říká *výjimka* (anglicky *exception*). `ValueError` z tracebacku je jeden druh výjimky. Výjimku můžeš v kódu *zachytit* a říct, co se má stát místo pádu. Slouží k tomu dvojice `try` a `except`:

```python
def cena_v_kc(polozka):
    try:
        cena = float(polozka["cena"])
    except ValueError:
        return 0
    if polozka["mena"] == "EUR":
        return cena * KURZ_EUR
    return cena
```

Python zkusí (`try`) provést odsazený řádek. Když při tom vznikne `ValueError`, nespadne, ale provede blok `except`: funkce vrátí 0. S překlepem `59O` teď program vypíše:

```text
Celkem: 3114.00 Kč
```

Program nespadl. Jenže výsledek je špatně – chybí v něm karimatka za 590 Kč. A nic tě na to neupozornilo. Bez výjimky program aspoň hlasitě spadl a ty jsi věděl(a), že je něco v nepořádku. S takhle napsanou výjimkou máš tichou chybu: program vypadá, že funguje, ale nedělá, co má.

Z toho plyne důležité pravidlo: **výjimka má chybu ošetřit, ne schovat.** Když ti agent navrhne `try` a `except`, vždy se podívej, co se stane v bloku `except`. Pokud chybu jen potichu "spolkne", zeptej se, jak se o ní dozvíš.

## Balíčky: hotové nástroje od jiných

> **Kdy se to hodí:** Kurz eura je v programu napevno, ale skutečný kurz najdeš každý den na internetu. Aby si ho program stáhl sám, potřebuje umět mluvit s webem. Psát to od nuly by bylo zbytečné – někdo už to napsal za tebe.

`import csv` načítá nástroj, který je součástí Pythonu. Spoustu dalších nástrojů napsali jiní lidé a zdarma je sdílejí. Takovému hotovému kusu kódu se říká *balíček* (anglicky *package*). Je to jako koupit si v obchodě hotové nářadí místo toho, abys ho vyráběl(a) sám(a).

Balíčky se stahují z veřejného katalogu [PyPI](https://pypi.org/) a do projektu je přidáš nástrojem `uv`. Vyzkoušíš to na balíčku `requests`, který umí stahovat data z internetu.

### 1. Udělej ze složky projekt pro uv

Seznam balíčků projektu si uv vede v souboru `pyproject.toml`. V terminálu ve VS Code (pořád ve složce `nakup`) ho jednou vytvoř:

```bash
uv init --bare
```

Výstup:

```text
Initialized project `nakup`
```

### 2. Přidej balíček

```bash
uv add requests
```

uv stáhne `requests` i balíčky, které `requests` sám potřebuje, a zapíše ho do `pyproject.toml`. Otevři soubor ve VS Code, uvidíš v něm:

```text
dependencies = [
    "requests>=2.34.2",
]
```

Číslo verze se u tebe může lišit. V Exploreru přibude ještě soubor `uv.lock` s přesnými verzemi všech stažených balíčků a složka `.venv`, kam se balíčky uložily. Do obou ručně nezasahuj, spravuje je uv.

### 3. Jak requests funguje

Prohlížeč pošle webu *požadavek* (anglicky *request*) a web mu vrátí *odpověď*: obvykle stránku s obrázky a tlačítky. Balíček `requests` dělá totéž, jen odpověď nevykreslí, ale předá ji programu jako text. Nejlépe se to ukáže na webu, který odpovídá rovnou obyčejným textem, třeba [wttr.in](https://wttr.in/) s předpovědí počasí – hodí se před výletem s novým spacákem.

Vytvoř v Exploreru soubor `pocasi.py` a vlož do něj:

```python
import requests

odpoved = requests.get("https://wttr.in/Praha?format=%l:+%C+%t&lang=cs")
print(odpoved.status_code)
print(odpoved.text)
```

Spusť ho:

```bash
uv run pocasi.py
```

Výstup (počasí bude jiné):

```text
200
Praha: Zamračeno +15°C
```

- `requests.get(...)` stáhne obsah z adresy, stejně jako když ji zadáš do prohlížeče. Část za `?` říká webu, co přesně chceš: místo, popis počasí a teplotu, česky.
- `status_code` je číselný kód odpovědi. `200` znamená, že je všechno v pořádku, `404`, že stránka neexistuje.
- `text` je samotný obsah odpovědi. S ním už program pracuje jako s jakýmkoli jiným textem.

Otevři stejnou adresu i v prohlížeči. Uvidíš tam stejný řádek – program dostal přesně to, co web posílá.

Bez připojení k internetu `requests.get` spadne s výjimkou `requests.exceptions.ConnectionError`. Je to stejná chyba za běhu jako `ValueError` u překlepu v datech, jen tentokrát není problém v souboru, ale v síti. Na to se budeš ptát ve cvičení.

## Cvičení: Aktuální kurz eura

Kurz 1 EUR = 25 Kč je v programu napevno. Skutečný kurz se ale mění a Česká národní banka ho každý pracovní den zveřejňuje na webu. Nech agenta upravit program tak, aby si aktuální kurz stáhl sám. Než začneš, oprav v `nakup.csv` překlep `59O` zpátky na `590`.

Prompt pro agenta:

```text
Uprav nakup.py tak, aby eura převáděl aktuálním kurzem
z denního kurzovního lístku ČNB místo pevného kurzu 25 Kč.
Napiš co nejjednodušší kód a použij jen funkce a výjimky.
Celý kód se musí vejít na jednu stránku.
Ke stažení kurzu použij balíček requests.
```

Poslední tři věty v promptu nech. Bez nich agent snadno napíše dlouhý kód s konstrukcemi a balíčky, které zatím neznáš, a ty bys ho nemohl(a) zkontrolovat. Balíček `requests` už v projektu máš, agent ho tedy nemusí instalovat. Pokud bude chtít spustit `uv add` s jiným balíčkem, zeptej se ho nejdřív proč.

Pak výsledek ověř:

1. Spusť program. Jaký kurz použil? Porovnej ho s kurzem eura na [webu ČNB](https://www.cnb.cz/cs/financni-trhy/devizovy-trh/kurzy-devizoveho-trhu/kurzy-devizoveho-trhu/).
2. Spočítej ručně, kolik má nákup stát: 2 129 Kč + 63 EUR × aktuální kurz. Shoduje se to s výstupem?
3. Vypni Wi-Fi a spusť program znovu. Spadne s tracebackem, nebo něco vypíše? Dozvíš se, že kurz chybí, nebo program potichu počítá s nulou?
4. Zapni Wi-Fi a v kódu změň adresu kurzovního lístku na chybnou. Nejdřív v názvu webu (`cnb.cz` na `cnb.czz`), pak na konci adresy (`denni_kurz.txt` na `denni_kurz.tx`). Po každé změně program spusť. Co se stalo? Je to pokaždé stejná chyba jako bez Wi-Fi? Nakonec adresu vrať.

Program je pořád deterministický, jen do něj přibyl vstup, který se každý den mění: kurz. Proto už nevypíše každý den stejný součet.

**Co když ČNB neodpoví?** Adresa, ze které si program bere data, je *API* (anglicky *application programming interface*): rozhraní, přes které spolu mluví programy, ne lidé. Když je API nedostupné, může program reagovat několika způsoby:

- **Skončit s chybou:** vypíše srozumitelnou zprávu, že kurz nejde stáhnout, a žádný součet nevypíše.
- **Použít záložní kurz:** počítá s pevným kurzem 25 Kč a upozorní, že výsledek je jen odhad.
- **Použít poslední známý kurz:** při každém úspěšném stažení si kurz uloží do souboru a při výpadku použije ten, s upozorněním, z jakého dne je.

Rozmysli si, která varianta se hodí pro program na hrubý odhad ceny nákupu a která pro firemní software, který potřebuje přesný kurz (třeba pro účetnictví). Kterou variantu zvolil tvůj agent?

```exercise
id: aktualni-kurz
revision: 1
title: Aktuální kurz eura
fields:
  - id: prompt
    label: Použitý prompt
  - id: zmeny
    label: Co agent změnil
    guidance: Kterou funkci přidal nebo upravil? Přidal do pyproject.toml nějaký další balíček?
  - id: overeni
    label: Kurz a výsledek
    guidance: Jaký kurz program použil? Shoduje se s webem ČNB? Sedí tvůj ruční výpočet s výstupem?
  - id: bez-internetu
    label: Co se stalo bez internetu
    guidance: Spadl program, nebo vypsal srozumitelnou zprávu? Je to ošetření chyby, nebo její schování?
  - id: chybna-adresa
    label: Co se stalo s chybnou adresou
    guidance: Jak se program choval s chybným názvem webu a jak s chybným koncem adresy? Lišilo se to?
  - id: varianty
    label: Co dělat, když API ČNB nefunguje
    guidance: Kterou variantu bys zvolil(a) pro hrubý odhad ceny a kterou pro firemní software? Proč? Co je v každém případě horší, žádný výsledek, nebo nepřesný výsledek?
```
