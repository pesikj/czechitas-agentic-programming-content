---
id: testovani
title: Testování
---

# Testování: jak poznáš, že aplikace pořád funguje

V lekci 05 psal agent testy podle postupu TDD a ty jsi je spouštěl(a) příkazem `test`. Dnes se podíváš, co v nich je, jaké druhy testů existují a jak je s agentem psát tak, aby opravdu něco hlídaly.

## Proč testovat

> **Kdy se to hodí:** Požádáš agenta, aby u obchodního případu zobrazoval i jméno obchodníka. Agent změní model, formulář a dvě šablony. Nová funkce funguje, jenže formulář pro přidání firmy se přestal ukládat. Zjistíš to až za týden, když si obchodníci stěžují, že nové firmy mizí.

Po každé změně bys mohl(a) celou aplikaci proklikat ručně: přidat firmu, přidat obchodní případ, zkusit špatný e-mail, zkontrolovat seznamy. U CRM je to pět minut, u větší aplikace hodina. A po desáté změně za den to přestaneš dělat.

*Automatický test* je program, který tohle proklikávání udělá za tebe. Každý test má tři kroky:

1. **Připrav** – vytvoř situaci, třeba firmu s IČO `25596641`.
2. **Proveď** – udělej akci, třeba odešli formulář.
3. **Ověř** – zkontroluj výsledek, třeba že firma je v databázi a na stránce se seznamem.

Testy spustíš jedním příkazem a za pár vteřin víš, jestli všechno, co dřív fungovalo, funguje i teď. Program je deterministický (víš z lekce 02), takže se stejným vstupem musí dát pokaždé stejný výsledek. Přesně tohle test hlídá.

Při práci s agentem jsou testy ještě důležitější než jindy. Agent mění mnoho souborů najednou a ty nemůžeš každý řádek předem vyzkoušet. Testy jsou síť, která zachytí, co agent rozbil, i na místech, kde jsi to nečekal(a).

## Tři druhy testů

Testy se dělí podle toho, jak velkou část aplikace najednou zkoušejí:

| Druh | Co zkouší | Příklad v CRM | Rychlost | Kolik jich psát |
|---|---|---|---|---|
| **Jednotkový** (*unit test*) | jednu malou část kódu, třeba jednu funkci, bez databáze a prohlížeče | funkce na kontrolu IČO | tisíciny vteřiny | nejvíc |
| **Integrační** (*integration test*) | spolupráci víc částí: formulář, view, databázi a šablonu | odeslání formuláře uloží firmu a ta se objeví v seznamu | setiny vteřiny | středně |
| **End-to-end** (zkráceně *E2E*) | celou aplikaci tak, jak ji používá člověk, ve skutečném prohlížeči | test v Playwright vyplní formulář a klikne na tlačítko | vteřiny | nejméně |

Představ si to jako kontrolu auta. Jednotkový test vyzkouší, jestli svítí jedna žárovka. Integrační test vyzkouší, jestli se po sešlápnutí brzdy rozsvítí brzdová světla. End-to-end test je zkušební jízda.

Čím větší část aplikace test zkouší, tím víc chyb najde, ale tím je pomalejší a křehčí: rozbije ho i přejmenované tlačítko. Proto se testů píše nejvíc jednotkových a nejméně end-to-end. Takovému rozložení se říká *testovací pyramida*.

## Testy v CRM

Testy, které agent napsal v lekci 05, najdeš v souboru `obchod/tests.py`. Od minulé lekce běží CRM v Dockeru, a proto i testy spouštíš v kontejneru `web`. Spusť aplikaci (`docker compose up`) a v druhém terminálu:

```bash
docker compose exec web uv run python manage.py test
```

Výstup (počet testů se bude lišit):

```text
Found 12 test(s).
Creating test database for alias 'default'...
System check identified no issues (0 silenced).
............
----------------------------------------------------------------------
Ran 12 tests in 0.214s

OK
Destroying test database for alias 'default'...
```

Každá tečka je jeden test, který prošel. Všimni si řádků `Creating test database` a `Destroying test database`. Django pro testy vytvoří samostatnou prázdnou *testovací databázi* a po testech ji smaže. Tvoje skutečné firmy a obchodní případy test nikdy nezmění.

Otevři `obchod/tests.py` a projdi ho. Každá metoda, která začíná `test_`, je jeden test. Název by měl říkat, co test hlídá, třeba `test_firma_bez_nazvu_nejde_ulozit`.

## Jednotkové testy

> **Kdy se to hodí:** Obchodník při přepisování z Excelu zadá IČO `25596642` místo `25596641`. CRM ho přijme, protože kontroluje jen to, že má IČO osm znaků. Za měsíc pošle faktura firmě, která neexistuje.

IČO má kontrolní číslici: poslední číslice se dopočítá z prvních sedmi. Překlep v jedné číslici se tak skoro vždy pozná. Kontrolu napíšeš jako samostatnou funkci, která dostane text a vrátí `True` nebo `False`. Takovou funkci jde otestovat úplně sama, bez databáze a bez formuláře. To je jednotkový test.

Funkce v souboru `obchod/validace.py` může vypadat takhle:

```python
def je_platne_ico(ico):
    if len(ico) != 8 or not ico.isdigit():
        return False
    soucet = sum(int(ico[i]) * (8 - i) for i in range(7))
    kontrolni = (11 - soucet % 11) % 10
    return kontrolni == int(ico[7])
```

Nemusíš rozumět výpočtu. Důležité je, že funkce dostane vstup a vrátí výstup a nic jiného nedělá. Jednotkové testy v `obchod/tests.py`:

```python
from django.test import SimpleTestCase

from obchod.validace import je_platne_ico


class JePlatneIcoTest(SimpleTestCase):
    def test_platne_ico(self):
        self.assertTrue(je_platne_ico("25596641"))

    def test_spatna_kontrolni_cislice(self):
        self.assertFalse(je_platne_ico("25596642"))

    def test_kratke_ico(self):
        self.assertFalse(je_platne_ico("1234"))

    def test_pismeno_v_ico(self):
        self.assertFalse(je_platne_ico("2559664A"))
```

- `SimpleTestCase` je druh testu v Djangu, který nepoužívá databázi. Proto je nejrychlejší.
- `assertTrue(...)` a `assertFalse(...)` ověří, že funkce vrátila `True`, nebo `False`. Když ne, test selže.
- Každý test zkouší jeden případ. Dobré testy nezkoušejí jen správný vstup, ale i chybné a hraniční: krátké IČO, písmeno, špatnou kontrolní číslici.

### Jak vypadá neúspěšný test

Když se ve funkci něco rozbije, třeba agent omylem změní `% 11` na `% 10`, test selže:

```text
F...
======================================================================
FAIL: test_platne_ico (obchod.tests.JePlatneIcoTest.test_platne_ico)
----------------------------------------------------------------------
Traceback (most recent call last):
  File "/app/obchod/tests.py", line 8, in test_platne_ico
    self.assertTrue(je_platne_ico("25596641"))
AssertionError: False is not true

----------------------------------------------------------------------
Ran 4 tests in 0.002s

FAILED (failures=1)
```

Výpis čteš stejně jako traceback z lekce 03, odspodu: `FAILED (failures=1)` říká, že jeden test selhal. Nad tím je, který (`test_platne_ico`), na kterém řádku a proč: funkce vrátila `False` u IČO, které je platné. Písmeno `F` na prvním řádku označuje neúspěšný test, tečky ty, které prošly.

### Funkce přes TDD s agentem

Tuhle funkci nemusíš psát sám(a). Zadáš ji agentovi a Superpowers ho povede postupem TDD z lekce 05: nejdřív testy, pak kód.

Prompt pro agenta:

```text
Použij skill brainstorming. Chci, aby formulář firmy kontroloval IČO:
musí mít 8 číslic a správnou kontrolní číslici podle pravidel pro IČO.
Kontrolu napiš jako samostatnou funkci je_platne_ico v obchod/validace.py.
Chci jednotkové testy funkce i integrační test formuláře, který ověří,
že firmu s neplatným IČO nejde uložit a že se pod polem zobrazí chyba
"Neplatné IČO".
Testy spouštím příkazem docker compose exec web uv run python manage.py test.
```

Je to malá změna, a tak se brainstorming nejspíš domluví s tebou jen v chatu a hned přejde k plánu. Ve výpisu práce agenta sleduj, jestli opravdu nejdřív spustil testy a viděl je selhat. Teprve pak má smysl, že prošly.

## Integrační testy

> **Kdy se to hodí:** Funkce `je_platne_ico` funguje a její testy prochází. Agent ji ale zapomněl zapojit do formuláře, takže CRM dál přijímá jakékoli IČO. Jednotkový test to nepozná, protože zkouší jen samotnou funkci.

Integrační test ověřuje, že části aplikace spolu správně spolupracují. V Djangu k tomu slouží *testovací klient* (`self.client`): program, který se chová jako prohlížeč bez obrazovky. Pošle aplikaci požadavek, třeba odeslaný formulář, a dostane odpověď, tedy HTML stránku. Mezitím projde celou cestou: adresou, view, formulářem, modelem, databází i šablonou.

```python
from django.test import TestCase

from obchod.models import Firma


class NovaFirmaTest(TestCase):
    def test_ulozeni_firmy(self):
        odpoved = self.client.post(
            "/firmy/nova/",
            {"nazev": "Pekárna U Lípy", "ico": "25596641", "stav": "nova"},
            follow=True,
        )
        self.assertEqual(Firma.objects.count(), 1)
        self.assertContains(odpoved, "Pekárna U Lípy")

    def test_neplatne_ico_nejde_ulozit(self):
        odpoved = self.client.post(
            "/firmy/nova/",
            {"nazev": "Pekárna U Lípy", "ico": "25596642", "stav": "nova"},
        )
        self.assertEqual(Firma.objects.count(), 0)
        self.assertContains(odpoved, "Neplatné IČO")
```

- `TestCase` (na rozdíl od `SimpleTestCase`) používá testovací databázi. Na začátku každého testu je prázdná.
- `self.client.post(...)` odešle formulář na adresu `/firmy/nova/`. Slovník obsahuje vyplněná pole. Názvy polí (`nazev`, `ico`, `stav`) odpovídají modelu a u tebe se můžou lišit.
- `follow=True` znamená "jdi i na stránku, kam tě aplikace po uložení přesměruje", tedy na seznam firem.
- `Firma.objects.count()` spočítá firmy v databázi, stejně jako v Django shellu v lekci 06.
- `assertContains(odpoved, "...")` ověří, že stránka obsahuje daný text. U druhého testu je to chybová hláška "Neplatné IČO", kterou jsi agentovi zadal(a). Kdyby test hledal jen slovo "IČO", prošel by vždycky, protože je na formuláři jako popisek pole.

Druhý test je stejně důležitý jako první. Kontroluje, že aplikace *odmítne*, co odmítnout má. Na takové testy se snadno zapomíná, a přitom právě v nich se schovává většina chyb.

## Testy v prohlížeči s Playwright

> **Kdy se to hodí:** Agent upraví vzhled stránky a tlačítko "Uložit" omylem schová pod menu. Integrační test projde, protože formulář posílá přímo a na tlačítko nekliká. Obchodník ale firmu uložit nedokáže.

Testovací klient Djanga stránku neotevře v prohlížeči. Nevidí, jestli je tlačítko vidět, jestli funguje JavaScript nebo jestli menu vede, kam má. To zvládne až *end-to-end test*: program spustí skutečný prohlížeč a aplikaci proklikne jako člověk.

[Playwright](https://playwright.dev/python/) je nástroj od Microsoftu, který ovládá prohlížeč z kódu. Umí otevřít stránku, vyplnit pole, kliknout na tlačítko a zkontrolovat, co se zobrazilo.

### Instalace

Playwright poběží na tvém počítači, mimo Docker, a bude zkoušet aplikaci, která běží v Dockeru. V terminálu ve VS Code, ve složce `crm`:

```bash
uv add --dev pytest-playwright
uv run playwright install chromium
```

- `uv add --dev` přidá balíček jako *vývojovou závislost* (anglicky *dev dependency*): potřebuješ ho jen při vývoji a testování, ne pro běh aplikace.
- `pytest-playwright` je Playwright spolu s *pytestem*, nástrojem na spouštění testů v Pythonu.
- `playwright install chromium` stáhne prohlížeč Chromium, který bude Playwright ovládat. Stahování má přes 100 MB a chvíli trvá.

### Nahraj test

Nejjednodušší způsob, jak napsat první test, je nechat ho nahrát. Spusť aplikaci (`docker compose up`) a v druhém terminálu:

```bash
uv run playwright codegen http://127.0.0.1:8000/firmy/nova/
```

Otevře se prohlížeč a vedle něj okno s kódem. Vyplň formulář a klikni na **Uložit**. Playwright každý tvůj krok zapíše jako řádek kódu. Nakonec v okně s kódem vyber jazyk **Python Pytest** a kód zkopíruj.

Ze zkopírovaného kódu vytvoř soubor `e2e/test_firmy.py` a doplň na konec kontrolu výsledku. Může vypadat takhle:

```python
from playwright.sync_api import Page, expect


def test_pridani_firmy(page: Page):
    page.goto("http://127.0.0.1:8000/firmy/nova/")
    page.get_by_label("Název").fill("Kavárna Playwright")
    page.get_by_label("IČO").fill("25596641")
    page.get_by_role("button", name="Uložit").click()
    expect(page.get_by_text("Kavárna Playwright")).to_be_visible()
```

- `page` je karta prohlížeče, kterou Playwright ovládá.
- `get_by_label("Název")` najde pole podle popisku, který vidí uživatel. `get_by_role("button", name="Uložit")` najde tlačítko podle textu. Popisky se u tebe můžou lišit, proto je výhodné test nahrát.
- `expect(...).to_be_visible()` ověří, že je text na stránce opravdu vidět.

### Spusť test

```bash
uv run pytest e2e
```

Výstup:

```text
============================= test session starts ==============================
collected 1 item

e2e/test_firmy.py .                                                      [100%]

============================== 1 passed in 2.31s ===============================
```

Prohlížeč běží bez okna, proto nic neuvidíš. Když chceš test sledovat, přidej přepínač `--headed`: `uv run pytest e2e --headed`.

Pozor na jeden rozdíl oproti testům v Djangu. Playwright zkouší skutečně běžící aplikaci s tvou databází, ne s testovací. Každé spuštění testu proto přidá do CRM firmu "Kavárna Playwright". Pro učení to nevadí. Ve větších projektech se testy v prohlížeči spouštějí proti samostatné kopii aplikace s vlastní databází.

## Testy a AI agent

Testy dnes často píše agent a je to dobře: napíše jich víc a rychleji než ty. Má to ale tři úskalí, na která si musíš dávat pozor.

**1. Test, který nic nehlídá.** Agent napíše test, který projde vždycky, třeba ověří jen to, že stránka existuje, a ne to, že je na ní uložená firma. Test vypadá dobře a dává zelený výsledek, ale chybu nenajde. Proto si každý důležitý test ověř: **rozbij kód a podívej se, jestli test selže.** Když neselže, nic nehlídá.

Prompt pro agenta:

```text
Ukaž mi, že test test_neplatne_ico_nejde_ulozit opravdu něco hlídá.
Dočasně vypni kontrolu IČO ve formuláři, spusť testy, ukaž mi výpis
a pak změnu vrať.
```

**2. Agent opraví test místo kódu.** Když test selže, nejsnazší cesta k zelenému výsledku je změnit test, ne kód. Agent to občas udělá: test "upraví", aby odpovídal chybnému chování. Proto v pull requestu vždycky zkontroluj, jestli se změnily i soubory s testy, a když ano, proč.

**3. Zelené testy nejsou hotová práce.** Testy ověřují jen to, co v nich je. Když agent špatně pochopil zadání, napíše špatný kód i testy, které ho potvrdí, a všechno svítí zeleně. Testy nenahradí tvou kontrolu, jestli aplikace dělá, co jsi chtěl(a). Proto po každé větší změně aplikaci aspoň krátce proklikej sám(a).

## Cvičení: Testy pro CRM

Přidej do CRM kontrolu IČO s testy všech tří druhů a ověř, že testy opravdu hlídají, co mají.

1. **Připrav se.** Udělej commit všech změn a vytvoř větev `kontrola-ico`. Spusť aplikaci a existující testy. Kolik jich je a prošly všechny?
2. **Kontrola IČO přes TDD.** Pošli agentovi prompt z části "Funkce přes TDD s agentem". Když se zeptá na worktree, odmítni. Po dokončení spusť testy sám(a).
3. **Rozbij funkci.** Ve funkci `je_platne_ico` změň `% 11` na `% 10` a spusť testy. Které selhaly? Pak změnu vrať.
4. **Ověř integrační test.** Nech agenta dokázat, že integrační test hlídá formulář (prompt z části "Testy a AI agent").
5. **Test v prohlížeči.** Nainstaluj Playwright, nahraj test přidání firmy a doplň do něj kontrolu výsledku. Pak nahraj druhý test: přidání firmy s neplatným IČO, která se nesmí uložit.
6. **Pull request.** Odešli větev, vytvoř pull request a v záložce **Files changed** zkontroluj, které testy přibyly a jestli agent nezměnil nějaký starší test.

```exercise
id: crm-testy
revision: 1
title: Testy pro CRM
fields:
  - id: pocet-testu
    label: Testy před a po
    guidance: Kolik testů měl projekt na začátku a kolik na konci? Prošly všechny?
  - id: tdd
    label: Postup agenta
    guidance: Spustil agent testy dřív, než napsal kód? Viděl je selhat?
  - id: rozbiti
    label: Co se stalo po rozbití kódu
    guidance: Které testy selhaly, když jsi změnil(a) % 11 na % 10? Které selhaly, když agent vypnul kontrolu ve formuláři?
  - id: playwright
    label: Testy v prohlížeči
    guidance: Co jsi musel(a) v nahraném kódu upravit? Prošel test s neplatným IČO?
  - id: pull-request
    label: Co jsi zkontroloval(a) v pull requestu
    guidance: Změnil agent nějaký starší test? Pokud ano, proč?
```

## Cvičení: Testy vlastního projektu

U vlastního projektu si nejdřív ujasni, co se testovat má, a teprve pak nech agenta testy psát.

1. **Sepiš scénáře.** Otevři `produkt.md` a návrh ze složky `docs/superpowers/specs/`. Podle sloupce Teď sepiš pět až osm vět ve tvaru "Když uživatel..., aplikace...", třeba "Když uživatelka zadá rezervaci na obsazený termín, aplikace ji odmítne a ukáže proč." Ulož je do souboru `testy.md`.
2. **Rozděl je.** U každého scénáře napiš, jestli se na něj hodí jednotkový, integrační, nebo end-to-end test, a proč. Hlídej pyramidu: end-to-end testů má být nejméně.
3. **Nech je napsat.** Pokud už máš první verzi aplikace, nech agenta napsat testy podle `testy.md`, jeden scénář za druhým, a u každého ověř, že test selže, když kód rozbiješ. Pokud aplikace ještě není, nech `testy.md` agentovi jako podklad pro plán: při psaní plánu mu řekni, ať z něj vychází.
4. Ulož `testy.md` commitem a odešli na GitHub.

```exercise
id: vlastni-projekt-testy
revision: 1
title: Testy vlastního projektu
fields:
  - id: scenare
    label: Scénáře
    guidance: Které scénáře jsi sepsal(a)? Je mezi nimi i takový, kdy aplikace něco odmítne?
  - id: druhy
    label: Rozdělení podle druhu testu
    guidance: Kolik scénářů je jednotkových, integračních a end-to-end? Proč?
  - id: vysledek
    label: Co agent napsal
    guidance: Pokud už aplikace existuje, které testy agent napsal a selhaly, když jsi kód rozbil(a)?
```
