---
id: plan
title: Plán a jeho provedení
---

# Plán a jeho provedení

Máš schválený návrh CRM. Teď z něj necháš agenta napsat plán, podle plánu aplikaci postavit a hotovou práci dostat přes pull request do `main`. Všechny tři kroky vede Superpowers: skill **writing-plans** napíše plán, **executing-plans** nebo **subagent-driven-development** ho provede a **finishing-a-development-branch** práci uzavře.

## Plán: z návrhu úkoly

> **Kdy se to hodí:** Návrh říká, *co* má CRM umět. Neříká ale, jaké soubory vzniknou, v jakém pořadí se budou psát a jak po každém kroku poznáš, že funguje. Když to agent neví předem, rozhoduje za pochodu a ty se v tom ztratíš.

Z lekce 02 znáš postup agentního programování: **Prozkoumej → Naplánuj → Naprogramuj → Otestuj → Ulož**. Brainstorming byl první krok, teď přichází plán. U celé aplikace je plán nejdůležitější krok: rozhoduje se v něm, jaké soubory vzniknou, co bude v každém z nich a v jakém pořadí se aplikace postaví. Změnit plán stojí jednu větu, změnit hotový kód stojí mnohem víc.

Po schválení návrhu agent sám přejde ke skillu writing-plans. Pokud to neudělá, napiš mu:

```text
Použij skill writing-plans a napiš ze schváleného návrhu plán.
```

Agent plán uloží do projektu, do složky `docs/superpowers/plans/`, třeba `docs/superpowers/plans/2026-10-22-crm.md`. Plán píše pro programátora, který projekt nikdy neviděl, proto je podrobný: obsahuje přesné cesty k souborům, celý kód a příkazy, kterými se každý krok ověří. Bývá dlouhý a celý ho číst nemusíš. Důležité části jsou na začátku a v nadpisech úkolů.

## Jak plán vypadá

Plán začíná hlavičkou: **Goal** (co se staví, jednou větou), **Architecture** (jak, dvěma třemi větami), **Tech Stack** (technologie) a **Spec** (odkaz na návrh, ze kterého plán vychází). Pak následují *úkoly* (anglicky *tasks*). Každý úkol končí něčím, co se dá samostatně ověřit. Zkrácená ukázka jednoho úkolu, tvůj plán se bude lišit:

```text
### Task 3: Modely Firma a ObchodniPripad

**Files:**
- Modify: `obchod/models.py`
- Test: `obchod/tests.py`

- [ ] Step 1: Napiš test, že firma bez názvu nejde uložit.
- [ ] Step 2: Spusť testy a ověř, že test selže.
      Run: uv run python manage.py test obchod
      Expected: FAILED
- [ ] Step 3: Napiš modely Firma a ObchodniPripad.
- [ ] Step 4: Vytvoř a proveď migraci, spusť testy znovu.
      Run: uv run python manage.py makemigrations && uv run python manage.py migrate
      Run: uv run python manage.py test obchod
      Expected: OK
- [ ] Step 5: Commit "Modely Firma a ObchodniPripad"
```

V plánu se objevuje několik pojmů z Djanga. Zatím ti stačí vědět, k čemu slouží:

- *Model* popisuje, jaké údaje se ukládají do databáze, třeba že firma má název, IČO a stav. *Migrace* je příkaz, kterým Django podle modelů upraví databázi.
- *View* (pohled) je funkce, která připraví stránku: načte data z databáze a předá je šabloně.
- *Šablona* (anglicky *template*) je HTML stránka s místy, kam Django doplní data.
- *Administrace* je hotové rozhraní Djanga, ve kterém můžeš data prohlížet a měnit bez vlastních formulářů.

### Testy: nejdřív test, potom kód

Všimni si, že úkol nezačíná kódem, ale *testem*. Test je krátký program, který kontroluje jiný kód: "když uložím firmu bez názvu, musí to skončit chybou". Superpowers vede agenta podle postupu *test-driven development* (zkráceně *TDD*, česky vývoj řízený testy): nejdřív napíše test, spustí ho a uvidí, že selže, protože kód ještě neexistuje. Pak napíše kód a test spustí znovu. Když teď projde, víš, že kód dělá, co má.

Testy všech částí aplikace spustíš jedním příkazem:

```bash
uv run python manage.py test
```

Výstup (počet testů se bude lišit):

```text
Ran 12 tests in 0.041s

OK
```

Psát testy sám(a) zatím nemusíš. Stačí, když víš, že existují, a umíš je spustit. Víc se o nich naučíš v lekci 07.

## Jak plán číst

Než plán schválíš, projdi ho stejně pozorně jako kód v pull requestu. Ptej se:

- **Odpovídá návrhu?** Pokrývají úkoly všechno, co je v návrhu? Nepřidal agent něco, co v návrhu není?
- **Rozumíš pořadí?** Dávají úkoly smysl v tomhle pořadí? Nejdřív projekt a modely, potom stránky a formuláře.
- **Rozumíš souborům?** Až budeš hledat, kde změnit údaje o firmě, budeš vědět, že v `obchod/models.py`?
- **Dá se každý úkol ověřit?** Má každý úkol test nebo příkaz s očekávaným výsledkem?

Když chceš v plánu něco změnit, napiš to agentovi, třeba "Administraci Djanga přidej hned po modelech, ať můžu data kontrolovat." Agent plán upraví. Pak plán výslovně schval.

## Proveď plán

Plán je jen nákres. Aplikace vznikne, až ho agent provede, a teprve teď zjistíš, jestli plán funguje.

### 1. Připrav větev

Agent bude práci ukládat commity a na konci ti ji nabídne poslat jako pull request. Připrav mu k tomu projekt:

1. Udělej commit všech změn a publikuj projekt `crm` na GitHub jako soukromý repozitář (**Publish Branch**, jako v lekci 04).
2. Vytvoř větev `prvni-verze` (klikni na název větve vlevo dole, **Create new branch...**).

Agent se tě může zeptat, jestli má vytvořit *worktree* (*Would you like me to set up an isolated worktree?*). Worktree je samostatná kopie projektu v jiné složce, ve které agent pracuje, aby nepřekážel tvé práci. Odpověz, že ne: pracuješ ve větvi `prvni-verze`, a to stačí.

### 2. Vyber způsob provedení

Po schválení plánu ti agent nabídne dva způsoby provedení:

| Způsob | Jak pracuje | Kdy ho zvolit |
|---|---|---|
| **Subagent-driven** (skill subagent-driven-development) | Na každý úkol pošle nového pomocného agenta (*subagenta*) a po každém úkolu nechá práci zkontrolovat dalším | Nejdůkladnější, ale nejvíc čerpá z limitu |
| **Inline** (skill executing-plans) | Všechny úkoly udělá sám v jedné konverzaci a na konci nechá zkontrolovat celou větev | Levnější, pro tenhle kurz stačí |

Pro CRM zvol **inline**. Z lekce 02 víš, že každá práce agenta čerpá z limitu předplatného, a subagent-driven ho spotřebuje několikanásobně víc.

### 3. Nech agenta pracovat

Agent provede všechny úkoly za sebou a mezi nimi se nezastavuje. U každého úkolu napíše test, kód, spustí testy a udělá commit. Zastaví se a zeptá jen tehdy, když chce udělat něco riskantního nebo když je plán tak nejasný, že by jen hádal. Celé provedení trvá obvykle 15–40 minut.

Zatím ho sleduj. Když se tě agent ptá na povolení příkazu, přečti si ho, stejně jako v lekci 02. V panelu Source Control v sekci **Graph** uvidíš, jak přibývají commity, jeden za každý úkol.

Když agent v plánu narazí na rozpor, sám rozhodne a zapíše si to jako *Ruling*: co rozhodl, proč a co by stálo, kdyby se spletl. Na konci se ho na tato rozhodnutí zeptej.

## Ověř výsledek

Superpowers agentovi zakazuje prohlásit práci za hotovou, dokud to neověří: musí ukázat výstup testů, ne jen napsat "hotovo". Ověř si to ale i sám(a). Agent mohl udělat přesně to, co je v plánu, a přesto něco chybí.

1. **Spusť testy.** `uv run python manage.py test` musí skončit `OK`.
2. **Spusť aplikaci.** V terminálu ve VS Code:

   ```bash
   uv run python manage.py runserver
   ```

   Otevři v prohlížeči http://127.0.0.1:8000/. Server běží, dokud ho nezastavíš klávesami `Ctrl C`. Dokud běží, terminál je obsazený, proto agenta spouštěj v druhém terminálu (ikona **+** v panelu terminálu).
3. **Proklikej ji.** Přidej firmu a obchodní případ přes formuláře. Zkus zadat špatný e-mail. Funguje to tak, jak je v návrhu?
4. **Přečti změny.** V sekci **Graph** projdi commity. Odpovídají úkolům z plánu?

Když něco nefunguje, napiš agentovi, co vidíš. Chybu najdeš v terminálu se serverem nebo přímo v prohlížeči, kde Django ukáže žlutou stránku s popisem chyby.

## Dokonči větev

Když jsou všechny úkoly hotové a testy prochází, agent použije skill finishing-a-development-branch a nabídne tři možnosti:

```text
Implementation complete. What would you like to do?
1. Merge back to main locally
2. Push and create a Pull Request
3. Keep the branch as-is (I'll handle it later)
```

- **Merge locally** – sloučí větev do `main` přímo na tvém počítači, bez review.
- **Push and create a Pull Request** – odešle větev na GitHub a vytvoří pull request.
- **Keep the branch** – nechá větev, jak je. Rozhodneš později.

Zvol **2**. Na GitHubu pak projdi pull request v záložce **Files changed**, stejně jako v lekci 04, sluč ho a ve VS Code se přepni do `main` a stáhni změny (**Sync Changes**). Pull request vytváří agent nástrojem `gh` (GitHub CLI). Pokud ho nemáš nainstalovaný, agent větev jen odešle a pull request vytvoříš na GitHubu sám(a) tlačítkem **Compare & pull request**.

## Cvičení: Postav CRM podle plánu

Projdi s agentem celý postup: plán ze schváleného návrhu, provedení ve větvi `prvni-verze`, ověření a pull request. Nakonec přidej tři firmy a dva obchodní případy, zastav server, spusť ho znovu a zkontroluj, že data zůstala.

```exercise
id: crm-podle-planu
revision: 1
title: Postav CRM podle plánu
fields:
  - id: zmeny-planu
    label: Co jsi v plánu změnil(a)
    guidance: Kolik úkolů plán měl? Rozuměl(a) jsi jejich pořadí? Upravil(a) jsi v plánu něco?
  - id: overeni
    label: Jak jsi ověřil(a) výsledek
    guidance: Prošly testy? Fungovala aplikace v prohlížeči tak, jak je v návrhu? Co bylo potřeba opravit?
  - id: odchylky
    label: Kde se agent od plánu odchýlil
    guidance: Jaká rozhodnutí (Ruling) agent udělal sám? Souhlasíš s nimi?
  - id: pull-request
    label: Pull request
    guidance: Kolik commitů a změněných souborů v něm bylo? Co jsi zkontroloval(a) v záložce Files changed?
```
