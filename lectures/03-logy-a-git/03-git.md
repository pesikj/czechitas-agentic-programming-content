---
id: git
title: Git
---

# Git: historie verzí programu

Log ti řekne, co program dělal. Co když ale program přestane fungovat proto, že se změnil kód? Pak potřebuješ vědět, co přesně se změnilo, a umět se vrátit k verzi, která fungovala.

## Co je Git

> **Kdy se to hodí:** Požádáš agenta, aby do `nakup.py` přidal převod dolarů. Agent upraví tři místa v kódu a program najednou počítá špatně i eura. Chceš vidět, co přesně změnil, a vrátit se k verzi, která fungovala.

Představ si, že píšeš diplomovou práci. Jednoho dne smažeš celou kapitolu, protože ji chceš napsat lépe, a pak zjistíš, že původní verze byla lepší. Nebo na stejném dokumentu pracujete dva a navzájem si přepisujete změny.

Přesně tohle řeší [Git](https://git-scm.com). Je to *systém pro správu verzí* (anglicky *version control system*): sleduje každou změnu v souborech projektu, pamatuje si historii všech uložených verzí a umožní ti se k nim kdykoli vrátit. Umí také sloučit práci více lidí dohromady.

Složce projektu, jejíž historii Git sleduje, se říká *repozitář* (anglicky *repository*). Tvůj projekt `nakup` se repozitářem stane, jakmile v něm Git zapneš (ukážeme si to níže ve VS Code). Git máš nainstalovaný z lekce 01 a funguje čistě na tvém počítači: historii si prohlédneš i bez internetu. Internet potřebuješ až tehdy, když chceš kód sdílet nebo zálohovat.

## Proč Git používat

- **Historie změn.** Každá uložená verze kódu zůstane zachovaná. Když nová úprava něco rozbije, podíváš se, co přesně se změnilo, a vrátíš se k verzi, která fungovala.
- **Záloha.** Kód uložený jen ve tvém počítači zmizí s jeho poruchou. S Gitem můžeš mít kopii i na serveru na internetu.
- **Spolupráce.** Na jednom projektu může pracovat víc lidí najednou. Git sleduje, kdo co změnil, a pomůže změny spojit.
- **Přenositelnost.** Projekt v Gitu si stáhneš na jakýkoli počítač nebo ho předáš jinému nástroji, třeba z Codexu v terminálu do Claude Code nebo do desktopové aplikace, a pokračuješ tam, kde jsi skončil(a).
- **Větve.** Chceš vyzkoušet novou funkci, aniž bys rozbil(a) program, který funguje? Zkoušíš ji v oddělené větvi a do hlavní verze ji přidáš, až když funguje (víc níže).

## GitHub, GitLab a další servery

Aby ses mohl(a) o kód dělit nebo ho zálohovat, potřebuješ místo na internetu, kde bude uložený. Takové kopii repozitáře na serveru se říká *vzdálený repozitář* (anglicky *remote repository*). Nejznámější služby, které je nabízejí:

- **[GitHub](https://github.com)** – největší platforma s miliony veřejných projektů, patří Microsoftu. Veřejné i soukromé repozitáře má zdarma. Účet sis na něm založil(a) v lekci 01.
- **[GitLab](https://gitlab.com)** – oblíbený ve firmách, protože si ho mohou provozovat na vlastním serveru a data neopustí firmu.
- **[Bitbucket](https://bitbucket.org)** – od firmy Atlassian, používají ho hlavně týmy, které pracují s jejími nástroji Jira a Confluence.

Všechny tři pracují s Gitem stejně, liší se doplňkovými funkcemi a cenou. GitHub je zároveň místem, kde žije spousta veřejně dostupného softwaru. Najdeš tam třeba i [balíček requests](https://github.com/psf/requests), který jsi minule přidal(a) do projektu.

## Git ve VS Code

Git se dá ovládat příkazy v terminálu, ale ty budeš pracovat hlavně ve VS Code. Ten má Git zabudovaný: změny, commity i historii uvidíš v přehledném panelu a většinu práce uděláš kliknutím. Agent naopak používá příkazy v terminálu, proto u každé operace najdeš i odpovídající příkaz. Až ho uvidíš v návrhu agenta, budeš vědět, co dělá.

### Výchozí kód projektu

Git si vyzkoušíš na projektu `nakup`. Program od agenta se u každého liší, a tak ať máte všichni stejný začátek, nahraď obsah souboru `nakup.py` tímto kódem. Je to verze z minulé lekce s aktuálním kurzem ČNB a s logy z předchozí části:

```python
import csv
import logging

import requests

ADRESA_KURZU = "https://www.cnb.cz/cs/financni-trhy/devizovy-trh/kurzy-devizoveho-trhu/kurzy-devizoveho-trhu/denni_kurz.txt"

logging.basicConfig(
    filename="nakup.log",
    level=logging.INFO,
    format="%(asctime)s %(levelname)s %(message)s",
    encoding="utf-8",
)


def stahni_kurz_eur():
    odpoved = requests.get(ADRESA_KURZU)
    odpoved.raise_for_status()
    for radek in odpoved.text.splitlines():
        casti = radek.split("|")
        if len(casti) == 5 and casti[3] == "EUR":
            return float(casti[4].replace(",", ".")) / int(casti[2])
    raise ValueError("Kurz eura v kurzovním lístku chybí")


def nacti_polozky(cesta):
    with open(cesta, encoding="utf-8", newline="") as soubor:
        polozky = list(csv.DictReader(soubor))
    logging.info("Načteno %d položek ze souboru %s", len(polozky), cesta)
    return polozky


def cena_v_kc(polozka, kurz_eur):
    try:
        cena = float(polozka["cena"])
    except ValueError:
        logging.error("Neplatná cena u položky %s: %r", polozka["polozka"], polozka["cena"])
        return 0
    if polozka["mena"] == "EUR":
        return cena * kurz_eur
    return cena


kurz_eur = stahni_kurz_eur()
polozky = nacti_polozky("nakup.csv")
celkem = 0
for polozka in polozky:
    celkem += cena_v_kc(polozka, kurz_eur)

logging.info("Celkem: %.2f Kč", celkem)
print(f"Kurz eura: {kurz_eur:.3f} Kč")
print(f"Celkem: {celkem:.2f} Kč")
```

Soubor `nakup.csv` vrať do původní podoby, bez překlepu `59O`:

```text
polozka,cena,mena
Batoh,1290,CZK
Spacák,45,EUR
Karimatka,590,CZK
Čelovka,18,EUR
Láhev na vodu,249,CZK
```

Spusť program:

```bash
uv run nakup.py
```

Výstup:

```text
Kurz eura: 24.325 Kč
Celkem: 3661.47 Kč
```

Kurz se každý pracovní den mění, takže tvoje čísla budou jiná. Celkem musí vyjít 2 129 Kč + 63 EUR krát kurz eura. Pokud program skončí chybou `ModuleNotFoundError: No module named 'requests'`, chybí v projektu balíček `requests`. Přidej ho jako v minulé lekci příkazem `uv add requests`.

### Panel Source Control

Otevři ve VS Code projekt `nakup`. Na levé liště klikni na ikonu **Source Control** (v české verzi **Správa zdrojového kódu**), tři kroužky spojené čarami. Otevřít ho můžeš i zkratkou `Ctrl Shift G` (Windows) nebo `⌃ Shift G` (macOS).

### Zapnutí Gitu v projektu

Projekt `nakup` zatím repozitář není, proto panel nabídne tlačítko **Initialize Repository**. Klikni na něj. VS Code tím v projektu zapne Git, stejně jako příkaz:

```bash
git init
```

### První nastavení: jméno a e-mail

Git používáš nejspíš poprvé, takže ho musíš jednou nastavit. Ke každému commitu Git připíše, kdo ho udělal, a proto potřebuje znát tvoje jméno a e-mail. Bez nich commit neuloží a VS Code tě upozorní hláškou *Make sure you configure your 'user.name' and 'user.email' in git*.

Otevři terminál ve VS Code (**Terminal → New Terminal**) a spusť dva příkazy. Jméno a e-mail v uvozovkách nahraď svými. Jako e-mail použij ten, se kterým máš účet na GitHubu, aby se ti tam commity později přiřadily:

```bash
git config --global user.name "Jana Nováková"
git config --global user.email "jana@example.com"
```

Přepínač `--global` znamená, že nastavení platí pro všechny projekty na tvém počítači. Stačí ho tedy udělat jednou, ne v každém projektu. Ověř, že se nastavení uložilo:

```bash
git config --global user.name
git config --global user.email
```

Výstup:

```text
Jana Nováková
jana@example.com
```

Jméno uvidí každý, kdo si tvůj projekt prohlédne na GitHubu, takže použij takové, které ti nevadí zveřejnit. Překlep opravíš tak, že příkaz spustíš znovu se správnou hodnotou.

## Základní operace

**Co se změnilo.** V panelu Source Control vidíš v sekci **Changes** seznam souborů, které se od posledního commitu změnily. Písmeno vedle souboru říká, co se s ním stalo: **U** je nový soubor, který Git zatím nesleduje, **M** změněný soubor a **D** smazaný soubor. Stejné písmeno a barvu vidíš i v panelu Explorer.

Když na soubor v seznamu klikneš, VS Code otevře porovnání: vlevo je poslední uložená verze, vpravo současná. Řádky, které zmizely, jsou červené, řádky, které přibyly, zelené. Právě tady zkontroluješ, co přesně změnil agent.

V terminálu ti totéž ukážou `git status` (seznam změněných souborů) a `git diff` (změněné řádky).

**Commit – uložení verze.** *Commit* je pojmenovaný snímek aktuálního stavu projektu. Je to jako uložení hry: v tuhle chvíli víš, že program funguje, a chceš mít možnost se sem vrátit.

Do pole nad seznamem změn napiš popis, třeba `Převod eur aktuálním kurzem ČNB`, a klikni na **Commit**. VS Code se zeptá, jestli má uložit všechny změny (*Would you like to stage all your changes and commit them directly?*). Zvol **Yes**. Seznam změn se vyprázdní: projekt je teď ve stavu posledního commitu.

Popis piš tak, abys i za měsíc věděl(a), co se v té verzi změnilo. V terminálu stejný commit uděláš dvěma příkazy. `git add .` vybere všechny změněné soubory a `git commit -m` vytvoří snímek s popisem:

```bash
git add .
git commit -m "Převod eur aktuálním kurzem ČNB"
```

**Historie.** V dolní části panelu Source Control je sekce **Graph** se seznamem commitů od nejnovějšího. Kliknutím na commit uvidíš, které soubory se v něm změnily, a kliknutím na soubor jeho změněné řádky. V terminálu vypíše historii `git log`.

**Zahození změny.** Když se úprava nepovede a commit ještě nemáš, najeď v sekci **Changes** myší na soubor a klikni na šipku zpět (**Discard Changes**). Soubor se vrátí do stavu z posledního commitu. Pozor, zahozené změny už nevrátíš.

**Push – odeslání na server.** *Push* odešle tvoje commity z počítače do vzdáleného repozitáře, třeba na GitHub. Ostatní lidé nebo jiné nástroje si je pak mohou stáhnout. Ve VS Code k tomu slouží tlačítko **Sync Changes** v panelu Source Control, které zároveň stáhne změny ze serveru. Tlačítko se objeví, až je projekt propojený se vzdáleným repozitářem (viz další část). V terminálu:

```bash
git push
```

**Pull – stažení změn ze serveru.** *Pull* stáhne do počítače commity, které na server poslal někdo jiný, nebo ty sám(a) z jiného počítače. Ve VS Code to udělá stejné tlačítko **Sync Changes**. V terminálu:

```bash
git pull
```

**Clone – stažení celého repozitáře.** *Clone* použiješ, když chceš na svém počítači pracovat s projektem, který zatím máš jen na serveru. Stáhne celý kód včetně kompletní historie. Ve VS Code otevři paletu příkazů (`Ctrl Shift P` na Windows, `⌘ Shift P` na macOS), napiš `Git: Clone`, vlož adresu repozitáře a vyber složku, kam se má projekt stáhnout. Adresu najdeš na GitHubu pod tlačítkem **Code**. V terminálu:

```bash
git clone https://github.com/psf/requests.git
```

Git vytvoří složku `requests` s celým projektem.

## Publikování projektu na GitHubu

> **Kdy se to hodí:** Program `nakup` máš zatím jen ve svém počítači. Chceš mít zálohu pro případ, že se počítač porouchá, a chceš projekt otevřít i na jiném počítači nebo v Codexu na webu.

Zatím jsou všechny tvoje commity jen v tvém počítači. Aby se dostaly na GitHub, musíš na něm vytvořit vzdálený repozitář a propojit ho s projektem. VS Code obojí udělá najednou.

### Veřejný, nebo soukromý repozitář?

Při publikování si vybereš, kdo repozitář uvidí:

- **Soukromý** (*private*) repozitář vidíš jen ty a lidé, které do něj sám(a) pozveš. Hodí se pro rozpracované projekty, cvičení a cokoli, co nechceš ukazovat.
- **Veřejný** (*public*) repozitář si může prohlédnout a stáhnout kdokoli na internetu, včetně celé historie commitů. Hodí se pro projekty, které chceš ukázat, třeba v portfoliu, nebo sdílet s ostatními. Upravovat ho ale mohou jen lidé, kterým to povolíš.

Pokud si nejsi jistý(á), zvol soukromý. Později ho můžeš na GitHubu změnit na veřejný (**Settings → Change visibility**). Opačně to tak jednoduché není: co jednou bylo veřejné, si už mohl někdo stáhnout. Proto nikdy nedávej do repozitáře hesla, API klíče ani osobní údaje, a to ani do soukromého.

### Publikování krok za krokem

1. Udělej commit všech změn, aby byl seznam **Changes** prázdný.
2. V panelu Source Control klikni na tlačítko **Publish Branch**.
3. VS Code se zeptá, jestli se smí přihlásit na GitHub (*The extension 'GitHub' wants to sign in using GitHub*). Klikni na **Allow**. Otevře se prohlížeč, přihlas se účtem z lekce 01 a potvrď přístup tlačítkem **Authorize Visual Studio Code**. Pak se vrať do VS Code. Tohle uděláš jen poprvé.
4. Nahoře se objeví nabídka s názvem repozitáře (předvyplní se název složky, `nakup`) a dvěma možnostmi: **Publish to GitHub private repository** a **Publish to GitHub public repository**. Vyber soukromý.
5. Po chvíli VS Code ohlásí, že projekt publikoval, a nabídne tlačítko **Open on GitHub**. Klikni na něj.

Na GitHubu uvidíš soubory projektu a nahoře u názvu označení **Private**. Klikni na počet commitů a uvidíš stejnou historii jako v sekci **Graph** ve VS Code.

Od teď je projekt propojený. Když uděláš další commit, odešleš ho na GitHub tlačítkem **Sync Changes**.

## Větev, pull request a merge

> **Kdy se to hodí:** Na výlet do Londýna a do USA si kupuješ další vybavení a ceny máš v librách a dolarech. Chceš, aby program převáděl i tyhle měny, ale nechceš riskovat, že rozbiješ verzi, která správně počítá koruny a eura.

*Větev* (anglicky *branch*) je samostatná linie historie projektu, ve které můžeš zkoušet změny bez dopadu na hlavní verzi. Hlavní větev se obvykle jmenuje `main`. Představ si ji jako kopii rozepsaného dokumentu, do které zkoušíš úpravy. Když se povedou, přeneseš je do originálu. Když ne, kopii zahodíš.

Projdeme celý postup na jedné malé funkci: převodu dalších měn. Začni s projektem publikovaným na GitHubu a s prázdným seznamem **Changes**.

### 1. Vytvoř větev

Ve VS Code vidíš název aktuální větve vlevo dole ve stavovém řádku, teď `main`. Klikni na něj, zvol **Create new branch...**, napiš název `dalsi-meny` a potvrď klávesou Enter. Ve stavovém řádku se teď ukáže `dalsi-meny`. V terminálu:

```bash
git switch -c dalsi-meny
```

Všechno, co teď změníš a uložíš commitem, bude jen ve větvi `dalsi-meny`. Větev `main` zůstane, jak byla.

### 2. Přidej funkci a ulož ji

Otevři `nakup.csv` a přidej na konec dva řádky:

```text
Pláštěnka,25,GBP
Kšiltovka,19,USD
```

Spusť agenta v terminálu ve VS Code.

Prompt pro agenta:

```text
Uprav nakup.py tak, aby kromě eur převáděl i ostatní měny
z denního kurzovního lístku ČNB, třeba libry (GBP) a dolary (USD).
Kód nech co nejjednodušší a použij jen funkce a výjimky.
```

Spusť program a zkontroluj, že u pláštěnky a kšiltovky počítá s kurzem z lístku ČNB. Tvůj kód se může od kódu ostatních lišit, důležité je, aby výsledek odpovídal ručnímu výpočtu. Pak v panelu Source Control proklikej změněné soubory a udělej commit s popisem `Převod dalších měn`.

### 3. Vytvoř pull request

Větev je zatím jen ve tvém počítači. Klikni v panelu Source Control na **Publish Branch** a VS Code ji odešle na GitHub (v terminálu `git push -u origin dalsi-meny`).

*Pull request* (zkráceně *PR*) je návrh, aby se změny z tvé větve přidaly do `main`. Je to místo, kde se o změně dá diskutovat dřív, než se stane součástí hlavní verze. Vytvoříš ho na GitHubu:

1. Otevři repozitář `nakup` na GitHubu. Nahoře se objeví žlutý pruh *dalsi-meny had recent pushes* s tlačítkem **Compare & pull request**. Klikni na něj. (Pokud pruh nevidíš, otevři záložku **Pull requests** a klikni na **New pull request**.)
2. Zkontroluj směr: **base: main ← compare: dalsi-meny**. Změny z `dalsi-meny` se mají přidat do `main`.
3. Napiš název, třeba `Převod dalších měn`, a do popisu krátce, co změna dělá a jak jsi ji ověřil(a): "Program převádí všechny měny z lístku ČNB. Ověřeno na librách a dolarech v nakup.csv."
4. Klikni na **Create pull request**.

### 4. Code review

*Code review* znamená, že změny před sloučením přečte někdo další a řekne, jestli jsou v pořádku. Ve firmách se do `main` obvykle nedostane nic, co nikdo nezkontroloval. Odhalí se tak chyby i místa, kterým by za půl roku nikdo nerozuměl.

V pull requestu otevři záložku **Files changed**. Uvidíš stejné porovnání jako ve VS Code: zelené řádky přibyly, červené zmizely. Když najedeš myší na řádek, objeví se modré **+** a k řádku můžeš napsat komentář, třeba "Co se stane, když měna v lístku ČNB není?".

Kdo kontroluje, nakonec klikne na **Review changes** a vybere jednu z možností:

- **Comment** – jen komentáře, bez rozhodnutí.
- **Approve** – změny jsou v pořádku a můžou se sloučit.
- **Request changes** – před sloučením je potřeba něco opravit.

Když je potřeba něco opravit, nepíšeš nový pull request. Přepneš se ve VS Code do větve `dalsi-meny`, opravíš kód (třeba s agentem), uděláš commit a klikneš na **Sync Changes**. Nový commit se v pull requestu objeví sám.

Na projektu teď pracuješ sám(a), takže review uděláš sobě: projdi si **Files changed** řádek po řádku, jako by kód psal někdo cizí. Ostatně psal: agent. Požádat o kontrolu můžeš i spolužáka nebo spolužačku, když je přidáš do repozitáře (**Settings → Collaborators**).

**Automatické akce.** K pull requestu se dají připojit akce, které GitHub spustí sám při každém novém commitu. Může třeba spustit testy, nebo nasadit zkušební verzi aplikace, kterou si před sloučením vyzkoušíš v prohlížeči. Jejich výsledek se ukáže přímo v pull requestu. Ukážeme si je později v kurzu.

### 5. Merge

Když je review hotové, klikni dole v pull requestu na **Merge pull request** a pak na **Confirm merge**. Změny se sloučí do `main` (anglicky *merge*) a pull request se označí jako **Merged**. GitHub nabídne tlačítko **Delete branch**. Větev už nepotřebuješ, takže ji smaž. Historie změn zůstane zachovaná v `main`.

### 6. Zpátky do main a pull

Teď je nová funkce ve větvi `main` na GitHubu, ale ve tvém počítači ještě ne. Merge proběhl na serveru a tvoje lokální `main` o něm neví.

Klikni ve VS Code na název větve vlevo dole a vyber `main`. Otevři `nakup.py`: převod dalších měn v něm není, máš tu verzi z doby před vytvořením větve. Teď si změny stáhni tlačítkem **Sync Changes** v panelu Source Control (nebo v nabídce **...** → **Pull**). V terminálu:

```bash
git switch main
git pull
```

Otevři `nakup.py` znovu, převod dalších měn už v něm je. Lokální větev `dalsi-meny` můžeš smazat: v paletě příkazů (`Ctrl Shift P` / `⌘ Shift P`) zvol **Git: Delete Branch...** a vyber ji. Na další funkci si založíš novou větev a celý postup zopakuješ.

## Git a AI agent

Git je pojítko mezi nástroji i mezi tebou a agentem. Pátý krok postupu agentního programování z minulé lekce, **Ulož**, v praxi znamená právě commit. Z toho plyne jednoduché pravidlo: **než necháš agenta měnit kód, udělej commit verze, která funguje.** Když se úprava nepovede, máš se kam vrátit.

Po práci agenta otevři panel Source Control a proklikej změněné soubory (v terminálu `git diff`). Uvidíš přesně ty řádky, které agent změnil, a ne jen jeho popis toho, co udělal. Tak poznáš, jestli změnil jen to, o co jsi žádal(a).

Codex i Claude Code umějí pracovat i přímo s repozitářem na GitHubu, bez tvého počítače: na webu jim zadáš úkol a výsledek ti předloží jako pull request ke schválení. I tady platí, co už znáš: změny si před sloučením přečti.

## Cvičení: Vlastní projekt na GitHubu

Teď celý postup projdeš sám(a) na vlastním malém projektu, od prvního commitu až po sloučený pull request.

**Vyber si projekt.** Stačí program na jednu stránku kódu. Pro inspiraci:

- **Počasí na výlet** – vypíše počasí ve třech městech, kam se chystáš, z webu [wttr.in](https://wttr.in), který už znáš z minulé lekce. *Nová funkce:* přidat teplotu na zítřek nebo upozornění, když bude pršet.
- **Kurz mé měny** – vypíše dnešní kurz měny, kterou potřebuješ, z kurzovního lístku ČNB. *Nová funkce:* přepočet několika částek nebo porovnání dvou měn.
- **Hvězdičky na GitHubu** – vypíše, kolik hvězdiček (oblíbení) má na GitHubu repozitář [psf/requests](https://github.com/psf/requests). Údaje vrací adresa `https://api.github.com/repos/psf/requests`. *Nová funkce:* porovnat několik repozitářů a seřadit je.
- **Deník výdajů** – sečte výdaje ze souboru `vydaje.csv` se sloupci `datum,popis,castka,kategorie`. Funguje bez internetu. *Nová funkce:* součet za každou kategorii zvlášť.
- **Losovač úkolů** – vylosuje z textového souboru `ukoly.txt` jeden domácí úkol na dnešek. *Nová funkce:* nelosovat stejný úkol dvakrát po sobě.

**1. Založ projekt.** V Dokumentech vytvoř novou složku (třeba `pocasi-na-vylet`) a otevři ji ve VS Code. Pokud budeš stahovat data z internetu, spusť v terminálu ve VS Code `uv init --bare` a `uv add requests`. Pak požádej agenta o program. Prompt doplň podle svého projektu:

```text
Napiš program pocasi.py, který vypíše aktuální počasí v Praze, Brně
a Vídni z webu wttr.in. Napiš co nejjednodušší kód a použij jen
funkce a výjimky. Celý kód se musí vejít na jednu stránku.
Ke stažení dat použij balíček requests.
```

Spusť program (`uv run pocasi.py`) a ověř, že výsledek sedí, třeba porovnáním s webem nebo s ručním výpočtem.

**2. Ulož a publikuj.** V panelu Source Control klikni na **Initialize Repository**, udělej první commit a projekt publikuj tlačítkem **Publish Branch**. Rozhodni se, jestli bude soukromý, nebo veřejný. Ať zvolíš cokoli, nesmí v něm být hesla ani osobní údaje.

**3. Nová funkce ve větvi.** Vytvoř větev s názvem podle funkce (třeba `zitrejsi-teplota`) a nech agenta funkci přidat. Program spusť a ověř, že funguje nová funkce i to, co fungovalo předtím. Udělej commit a větev odešli tlačítkem **Publish Branch**.

**4. Pull request a review.** Na GitHubu vytvoř pull request z tvé větve do `main` a napiš do popisu, co změna dělá a jak jsi ji ověřil(a). V záložce **Files changed** projdi všechny změněné řádky. Rozumíš každému? Změnil agent jen to, o co jsi žádal(a)? Pokud ne, oprav to ve větvi dalším commitem.

**5. Merge a pull.** Sluč pull request (**Merge pull request** → **Confirm merge**) a smaž větev na GitHubu. Ve VS Code se přepni zpátky do `main` a stáhni změny tlačítkem **Sync Changes**. Ověř, že nová funkce je v kódu a program ji umí.

**6. Zkontroluj historii.** Otevři v panelu Source Control sekci **Graph**. Měl(a) bys v ní vidět první commit, commit s novou funkcí a commit, kterým GitHub pull request sloučil (*Merge pull request #1...*). Klikni na commit s novou funkcí a podívej se, které řádky změnil.

```exercise
id: vlastni-projekt-na-githubu
revision: 1
title: Vlastní projekt na GitHubu
fields:
  - id: projekt
    label: Projekt a odkaz na repozitář
    guidance: Co program dělá? Je repozitář soukromý, nebo veřejný, a proč?
  - id: funkce
    label: Nová funkce a větev
    guidance: Jak se větev jmenuje, co agent přidal a jak jsi ověřil(a), že to funguje?
  - id: review
    label: Co jsi zjistil(a) při review
    guidance: Které soubory a řádky se změnily? Rozuměl(a) jsi všem? Musel(a) jsi něco opravit?
  - id: graph
    label: Commity v sekci Graph
    guidance: Jaké commity v historii vidíš a v jakém pořadí?
```
