---
id: programovani-v-dobe-ai
title: Programování v době AI
---

# Programování v době AI

Teď už víš, jak agent ovládá počítač přes terminál. Než ho necháš psát kód, ujasníme si, co to vlastně znamená *programovat* a jakou roli v tom dnes hraje umělá inteligence. Bez toho by práce s AI agentem připomínala zadávání úkolů v jazyce, kterému nerozumíš.

Celou dobu nás bude provázet jeden malý příklad: program, který sčítá ceny nákupu – nejdřív jen v korunách, později i v eurech. Na konci budeš umět popsat jeho logiku, poznat, v jakém jazyce je napsaný, a vysvětlit, jak bys ho postavil(a) s pomocí AI agenta.

## Nový projekt ve VS Code

> **Kdy se to hodí:** Program na sčítání nákupu bude mít víc souborů: kód, data, později i záznamy o chybách. Chceš je mít pohromadě na jednom místě, vidět je v editoru a spouštět je v terminálu, aniž bys je musel(a) hledat.

Než začneme, připravíme si *projekt*. Ve VS Code je projekt prostě složka (adresář), ve které jsou všechny soubory jedné aplikace. Když složku otevřeš ve VS Code, editor ti ukáže všechny její soubory, terminál ve VS Code se v ní rovnou spustí a v téže složce bude pracovat i agent. Do projektu `nakup` budeš ukládat všechno z této lekce.

### 1. Vytvoř složku

V terminálu přejdi do Dokumentů a vytvoř v nich složku `nakup`:

```bash
cd Documents
mkdir nakup
cd nakup
```

Příkaz `mkdir` (*make directory*) vytvoří novou složku. Tyhle příkazy fungují stejně v PowerShellu i v zsh.

### 2. Otevři složku ve VS Code

Nejrychleji to jde z terminálu, ve kterém právě jsi:

```bash
code .
```

Příkaz `code` spustí VS Code a tečka znamená "aktuální složka". VS Code se tedy otevře rovnou ve složce `nakup`.

Složku můžeš otevřít i bez terminálu. Ve VS Code klikni v horním menu na **File → Open Folder...** (v české verzi **Soubor → Otevřít složku...**), najdi v Dokumentech složku `nakup` a potvrď tlačítkem **Select Folder** (Windows) nebo **Open** (macOS).

### 3. Potvrď důvěru

Při prvním otevření se VS Code zeptá, jestli důvěřuješ autorům souborů ve složce (*Do you trust the authors of the files in this folder?*). Složku jsi právě vytvořil(a) sám(a), takže zvol **Yes, I trust the authors**. U složek stažených z neznámých zdrojů buď opatrnější – VS Code se ptá právě proto, že v nich může být kód, který se spustí sám.

### 4. Zorientuj se

V levém panelu **Explorer** (Průzkumník) uvidíš název složky `NAKUP`. Zatím je prázdná, soubory do ní přibudou během lekce.

Otevři terminál přímo ve VS Code: v menu zvol **Terminal → New Terminal** (**Terminál → Nový terminál**). Ve spodní části okna se objeví terminál – na Windows s PowerShellem, na macOS se zsh. Ověř, kde jsi:

```bash
pwd
```

Cesta na konci výpisu má končit složkou `nakup`. Od teď budeš všechny příkazy z lekce spouštět v tomhle terminálu.

Ukázky kódu z této části zatím spouštět nemusíš. Pokud si je chceš vyzkoušet, vytvoř si v Exploreru soubor `zkouska.py` (ikona nového souboru vedle názvu složky), vlož do něj kód a spusť ho příkazem `uv run zkouska.py`.

## 2. Programová logika

> **Kdy se to hodí:** Máš program, který sčítá ceny vybavení na výlet z českého e-shopu, a funguje bez chyby. Pak začneš nakupovat i v německém e-shopu a do seznamu přibudou ceny v eurech. Program dál běží, nic nehlásí – a přitom počítá nesmysly.

### Program je přesný postup

Počítač nic nedomýšlí. Udělá přesně to, co mu napíšeš – ne to, co jsi tím *myslel(a)*. Programová logika je dovednost rozložit úkol na malé, jednoznačné kroky.

Takovému postupu se říká *algoritmus* (anglicky *algorithm*). Funguje jako recept: má suroviny, kroky v daném pořadí a výsledek. Když v receptu chybí "osolit", polévka bude bez soli – a počítač se ani nezeptá.

### Když se změní data, ale ne kód

Na začátku nakupuješ jen v českém e-shopu. Všechny ceny jsou v korunách:

| Položka | Cena | Měna |
|---|---|---|
| Batoh | 1 290 | Kč |
| Karimatka | 590 | Kč |
| Láhev na vodu | 249 | Kč |

Program má jediný úkol: "sečti ceny". Výsledek 1 290 + 590 + 249 = 2 129 Kč je správně. Program funguje a nikdo na něj nesahá.

Pak přidáš dvě věci z německého e-shopu. Data se změnila – v tabulce jsou teď dvě měny:

| Položka | Cena | Měna |
|---|---|---|
| Batoh | 1 290 | Kč |
| Spacák | 45 | EUR |
| Karimatka | 590 | Kč |
| Čelovka | 18 | EUR |
| Láhev na vodu | 249 | Kč |

Program ale zůstal stejný. Dál dělá jen "sečti ceny", takže vezme čísla ze sloupce Cena a sečte je:

```text
1 290 + 45 + 590 + 18 + 249 = 2 192
```

Výsledek 2 192 je nesmysl. Nejsou to koruny ani eura – jsou to koruny a eura smíchané dohromady. Počítač ale nepozná, že je něco špatně. Sloupec Měna pro něj nic neznamená, dokud mu neřekneš, co s ním má dělat.

Kde se chyba vzala? Původní program měl v sobě skrytý předpoklad: "všechny ceny jsou v korunách". Nikde napsaný nebyl, protože dokud byla data jen v Kč, nebylo ho potřeba. Když se data změnila, předpoklad přestal platit – a kód o tom nevěděl.

### Oprava: řekni to počítači výslovně

Člověk by si měn všiml hned. Počítači to musíš napsat jako samostatný krok: "ceny v eurech nejdřív převeď na koruny". K tomu potřebuje ještě jeden údaj, který v tabulce vůbec není – *kurz*. Pro jednoduchost počítejme s kurzem 1 EUR = 25 Kč (skutečný kurz se mění každý den):

```text
Ceny v Kč:   1 290 + 590 + 249 = 2 129 Kč
Ceny v EUR:  45 + 18 = 63 EUR → 63 × 25 = 1 575 Kč
Celkem:      2 129 + 1 575 = 3 704 Kč
```

Teď výsledek dává smysl: nákup tě vyjde na 3 704 Kč. Rozdíl oproti 2 192 je přes 1 500 Kč – přesně tolik "zmizelo", protože program bral eura jako koruny.

Tohle je jádro programové logiky:

- Počítač dělá jen to, co mu výslovně řekneš. Všechno, co je pro člověka samozřejmé – že eura nejsou koruny, že je potřeba kurz – musíš do postupu napsat ty.
- Každý program počítá s nějakými předpoklady o datech. Když se data změní, zkontroluj, jestli předpoklady pořád platí, a uprav postup.

Úplně stejně to platí, když zadáváš úkol AI.

### Stavební kameny programu

Skoro každý program se skládá z několika stejných kousků. Ukážeme si je na programu s nákupem:

- **Vstup → zpracování → výstup.** Program něco dostane (ceny, měny a kurz), něco s tím udělá (převede eura a sečte) a něco vrátí (celkovou cenu v Kč). Když přemýšlíš o novém programu, začni otázkou: co do něj vstoupí a co z něj má vyjít? Tady se ukázalo, že s eury přibyl nový vstup – kurz.
- **Posloupnost.** Kroky se provádějí jeden po druhém, shora dolů. Ceny můžeš sečíst až potom, co jsi je převedl(a) na stejnou měnu.
- **Proměnná.** Krabička se štítkem, do které si program uloží hodnotu, aby ji mohl použít později – třeba `kurz_eur = 25`. Štítek je název, obsah krabičky se může měnit. Když se kurz změní, přepíšeš jedno číslo a celý výpočet sedí.
- **Rozhodování.** "Pokud je cena v EUR, vynásob ji kurzem. Jinak ji nech, jak je." Program se podle situace vydá jednou ze dvou cest.
- **Opakování.** "Pro každou položku nákupu..." Stejný krok se provede víckrát, aniž bys ho musel(a) psát znovu.

S těmito pěti kousky popíšeš překvapivě velkou část programů, které kolem sebe vidíš. Rozhodování a opakování si v Pythonu vyzkoušíš v dalších lekcích. Dnes stačí, když je v postupu poznáš.

### Pseudokód

Než začneš psát kód (nebo ho zadáš AI), sepiš si kroky obyčejnou češtinou. Takovému zápisu se říká *pseudokód* – vypadá jako program, ale nemusí dodržovat pravidla žádného jazyka. Pomáhá ti ujasnit si, co přesně chceš, dřív než řešíš, jak se to píše.

Pseudokód původního programu, kdy byly všechny ceny v korunách:

```text
1. Ulož ceny všech položek.
2. Sečti je a ulož výsledek do "celkem".
3. Vypiš: "Celkem: <celkem> Kč".
```

Při psaní pseudokódu se vyplatí u každého kroku zeptat: dávají data, se kterými tady pracuji, dohromady smysl? Právě tahle otázka by odhalila, že po přidání eur krok 2 sčítá koruny s eury.

Takhle vypadá pseudokód programu, který počítá i s eury. Používá rozhodování a opakování. Nemusíš ho zatím umět napsat v Pythonu, jen si všimni, jak se v textu poznají:

```text
Nastav celkem = 0.
Pro každou položku nákupu:
    Pokud je měna EUR:
        Přičti k celkem cenu × kurz_eur.
    Jinak:
        Přičti k celkem cenu.
Vypiš celkem v Kč.
```

Odsazení ukazuje, které kroky patří k sobě: co se opakuje pro každou položku a co se provede jen v jedné z cest. Stejně to bude fungovat i v Pythonu.

### Ověř postup na papíře

Postup si můžeš vyzkoušet ještě dřív, než existuje jediný řádek kódu. Projdi ho krok po kroku s konkrétními čísly a zapisuj si, co se děje. Takové tabulce se říká *trasovací tabulka*. Projdeme poslední pseudokód položku po položce:

| Položka | Cena | Měna | Cena v Kč | celkem |
|---|---|---|---|---|
| (začátek) | | | | 0 |
| Batoh | 1 290 | Kč | 1 290 | 1 290 |
| Spacák | 45 | EUR | 1 125 | 2 415 |
| Karimatka | 590 | Kč | 590 | 3 005 |
| Čelovka | 18 | EUR | 450 | 3 455 |
| Láhev na vodu | 249 | Kč | 249 | 3 704 |

Na konci je v proměnné `celkem` hodnota 3 704 – stejná jako při ručním výpočtu. Postup tedy funguje.

Když postup projdeš i s nepříjemnými situacemi, najdeš chyby dřív než počítač. Co když přidáš položku v dolarech? Postup s ní nepočítá – měna není EUR, takže by se dolary přičetly jako koruny. Byla by to stejná chyba jako na začátku: data se změnila, kód ne.

### Z pseudokódu do Pythonu

Podívejme se, jak celý příběh vypadá v Pythonu. Zatím ho nemusíš spouštět – stačí si všimnout, že řádky odpovídají krokům pseudokódu. Původní program pro nákup v korunách:

```python
batoh = 1290
karimatka = 590
lahev = 249

celkem = batoh + karimatka + lahev
print("Celkem:", celkem, "Kč")
```

Výstup:

```text
Celkem: 2129 Kč
```

Pak přidáš dvě položky z německého e-shopu. Dopíšeš je do programu a do součtu, ale jinak kód necháš, jak byl:

```python
batoh = 1290
spacak = 45       # EUR
karimatka = 590
celovka = 18      # EUR
lahev = 249

celkem = batoh + spacak + karimatka + celovka + lahev
print("Celkem:", celkem, "Kč")
```

Text za znakem `#` je *komentář* – poznámka pro člověka, kterou Python přeskočí. Komentář sice říká, že spacák je v eurech, ale Python ho nečte, takže to neví.

Výstup:

```text
Celkem: 2192 Kč
```

Program proběhne bez jediné chyby a dokonce za výsledek napíše "Kč" – a přesto je špatně. Na takové chyby si dávej pozor: počítač tě neupozorní, protože z jeho pohledu je všechno v pořádku.

Správná verze má převod měny přímo v kódu:

```python
kurz_eur = 25     # 1 EUR = 25 Kč

batoh = 1290
spacak = 45 * kurz_eur
karimatka = 590
celovka = 18 * kurz_eur
lahev = 249

celkem = batoh + spacak + karimatka + celovka + lahev
print("Celkem:", celkem, "Kč")
```

Výstup:

```text
Celkem: 3704 Kč
```

Rozdíl oproti chybné verzi je jeden nový řádek s kurzem a dvakrát `* kurz_eur` u položek v eurech. Právě tyhle změny jsou výsledkem tvého přemýšlení o datech, ne psaní kódu.

### Výhoda: program je předvídatelný

Všimni si jedné důležité věci. Výsledek 3 704 Kč jsi znal(a) dřív, než Python cokoli spustil – spočítal(a) jsi ho ručně v trasovací tabulce. A Python vypsal přesně to samé.

Program je *deterministický* (anglicky *deterministic*): se stejnými vstupy udělá pokaždé přesně to samé a dá pokaždé stejný výsledek. Postup je pevně daný v kódu. Spustíš-li program s nákupem dnes, zítra nebo za rok, vždy vypíše `Celkem: 3704 Kč`. Výsledek se změní jen tehdy, když změníš data nebo kód.

Z toho plyne velká výhoda: **když kódu rozumíš, umíš předpovědět jeho výsledek.** Nemusíš programu slepě věřit. Projdeš kroky, spočítáš si, co má vyjít, a porovnáš to se skutečným výstupem. Když se liší, víš jistě, že je někde chyba – v kódu, nebo v tvé představě o něm.

Díky tomu jsme taky dokázali chybu s eury najít. Věděli jsme, co má vyjít (3 704 Kč), a program vypsal něco jiného (2 192 Kč). U AI to tak nefunguje – na stejnou otázku ti může pokaždé odpovědět trochu jinak. Proto je tak cenné, když výsledek práce AI skončí jako kód, kterému rozumíš a jehož chování umíš předpovědět.

### Proč se logika hodí i při práci s AI

Možná si říkáš, proč se tím zabývat, když kód napíše AI. Představ si, že agenta požádáš: "Přidej do nákupu spacák za 45 EUR a čelovku za 18 EUR." Agent položky poslušně přidá – a nemusí si všimnout, že součet pod nimi počítá jen s korunami. Přesně tak vznikla chyba z našeho příkladu.

Proto se programová logika hodí dvakrát. Když agentovi dáš jasný postup ("eura převeď kurzem 25 Kč"), dostaneš přesnější kód. A když kód napíše sám, můžeš ho porovnat se svými kroky a zkontrolovat, jestli nic nevynechal nebo nepřidal něco, o co jsi nežádal(a).

Programová logika je tedy dovednost, kterou AI nenahradí. Ty víš, co má program dělat a co znamenají data, se kterými pracuje. AI ti pomůže to zapsat.

## 3. Programovací jazyky

Postup už umíš sepsat česky. Počítač ale češtině nerozumí – potřebuje ho dostat v jazyce, který zná.

> **Kdy se to hodí:** Agent ti napíše program na sčítání nákupu. Podle vzhledu kódu poznáš, v jakém jazyce je napsaný – a jestli je to ten, který jsi chtěl(a).

### Zdrojový kód

Každá aplikace, webová stránka nebo hra je v jádru text. Speciálně formátovaný text, kterému rozumí počítač. Tomuto textu se říká *zdrojový kód* (anglicky *source code*).

Zdrojový kód si můžeš otevřít v obyčejném textovém editoru, třeba ve Visual Studio Code, které máš nainstalované. Když AI agent "programuje", ve skutečnosti píše a upravuje právě takové textové soubory.

### Co je programovací jazyk

Aby počítač zdrojovému kódu rozuměl, musí být napsaný v *programovacím jazyce* (anglicky *programming language*). Ten určuje, jak se příkazy píšou a co znamenají – podobně jako gramatika určuje, jak se skládají české věty.

Pravidlům zápisu se říká *syntaxe* (anglicky *syntax*). Na rozdíl od člověka počítač neodpouští ani drobnost. Když v Pythonu zapomeneš uzavírací uvozovku, program se vůbec nespustí:

```python
print("Ahoj)
```

Výstup:

```text
  File "pozdrav.py", line 1
    print("Ahoj)
          ^
SyntaxError: unterminated string literal (detected at line 1)
```

Chybová hláška vypadá děsivě, ale říká užitečné věci: v jakém souboru a na jakém řádku je problém a co se stalo (neukončený text). Číst chybové hlášky se naučíš postupně v průběhu kurzu.

### Proč existuje tolik jazyků

Programovacích jazyků existují stovky. Vznikaly v různé době a pro různé účely, podobně jako různé nástroje v dílně: kladivem se dá zatlouct hřebík i rozbít ořech, ale na šroubek je lepší šroubovák. Některé jazyky jsou velmi rychlé, jiné snadno čitelné, další běží v prohlížeči nebo v pračce.

Dobrá zpráva je, že myšlenky z kapitoly o programové logice – vstup, výstup, proměnné, rozhodování a opakování – najdeš skoro ve všech. Když pochopíš logiku v jednom jazyce, druhý se naučíš mnohem rychleji.

### Čtyři jazyky, jeden program

Tady je stejný úkol – vypsat pozdrav – ve čtyřech jazycích. Všimni si, že myšlenka je pořád stejná, mění se jen zápis.

**Python** – čitelný, skoro jako angličtina. Používá se na automatizaci, práci s daty, AI a webové aplikace. **V tomhle kurzu budeme psát v Pythonu.**

```python
print("Ahoj, Czechitas!")
```

**JavaScript** – jazyk webu. Běží v prohlížeči a stará se o to, aby stránky reagovaly na klikání a formuláře. Dnes se používá i na serverech.

```javascript
console.log("Ahoj, Czechitas!");
```

**TypeScript** – JavaScript rozšířený o *typy*: u každé hodnoty předem říkáš, jestli je to text, číslo a podobně. Chyby se tak najdou dřív, než program spustíš. Před spuštěním se převádí na JavaScript. Často ho uvidíš ve větších webových aplikacích.

```typescript
const jmeno: string = "Czechitas";
console.log(`Ahoj, ${jmeno}!`);
```

**Rust** – moderní, velmi rychlý a bezpečný jazyk: hlídá chyby v práci s pamětí, které v jiných rychlých jazycích snadno vzniknou. Používá se třeba v prohlížečích nebo v nástrojích pro programátory – i `uv`, které máš nainstalované, je napsané v Rustu.

```rust
fn main() {
    println!("Ahoj, Czechitas!");
}
```

Porovnej Python s Rustem: v Pythonu stačí jeden řádek, v Rustu musí i ten nejjednodušší program mít kolem sebe funkci `main`. To je jeden z důvodů, proč je Python oblíbený u začátečníků – i u AI. Kód je krátký a dobře se čte, takže snáz zkontroluješ, co agent napsal.

### Co potřebuješ ke spuštění kódu

> **Kdy se to hodí:** Agent ti program na sčítání nákupu napíše v Rustu. Kód vypadá v pořádku, ale když ho chceš spustit, počítač hlásí, že příkaz nezná. Kód je hotový – jen ti chybí nástroj, který ho umí spustit.

Agent umí psát v jakémkoli jazyce. Napsat kód ale nestačí: abys ho mohl(a) spustit, musíš mít na počítači nainstalované nástroje pro daný jazyk. Počítač totiž sám rozumí jen velmi jednoduchým instrukcím a zdrojový kód se do nich musí nějak převést. Jazyky to řeší dvěma hlavními způsoby:

- **Interpretované jazyky** (Python, JavaScript) – potřebuješ *interpret* (anglicky *interpreter*), program, který čte tvůj kód a rovnou ho provádí. Pro Python je to interpret Pythonu, pro JavaScript například prohlížeč nebo Node.js.
- **Překládané jazyky** (Rust) – potřebuješ *překladač* (anglicky *compiler*), který kód nejdřív *přeloží* do spustitelného souboru (ve Windows s příponou `.exe`). Ten pak spustíš jako jakýkoli jiný program. Překlad chvíli trvá, ale výsledný program bývá rychlejší.

Interpret Pythonu už máš – nainstaloval(a) sis ho přes `uv` v lekci 01. Ověřit to můžeš v terminálu:

```bash
uv run python --version
```

Výstup (číslo verze se může lišit):

```text
Python 3.13.7
```

Překladač Rustu nainstalovaný nemáš, takže program v Rustu by ti nešel spustit. Proto je dobré jazyk volit podle toho, jaké nástroje máš. U Pythonu napíšeš kód a hned ho spustíš – to se při učení i při práci s agentem hodí.

### Jazyk v zadání pro agenta

Při práci s agentem jazyk vždy uveď v zadání. Když ho vynecháš, agent si může vybrat jiný, než jsi čekal(a) – třeba JavaScript, protože "aplikace" mu zní jako web.

Prompt pro agenta:

```text
Napiš v Pythonu program, který sečte ceny pěti položek nákupu.
Ceny jsou v Kč a v EUR. Eura převeď na koruny kurzem 1 EUR = 25 Kč
a vypiš celkovou cenu v Kč.
```

## 4. AI, vibe coding a agentní programování

Víš, co je program a v čem se píše. Dnes ho ale nemusíš psát celý sám(a) – velkou část kódu za tebe napíše AI. Pojďme si ujasnit, jak to funguje a jakou roli v tom máš ty.

### Co je umělá inteligence

> **Kdy se to hodí:** Zeptáš se ChatGPT, jak sečíst ceny nákupu v korunách a eurech, a během pár vteřin dostaneš funkční kód v Pythonu. Nikdo mu přitom nenapsal pravidlo "na otázku o nákupu odpověz tímhle kódem".

Představ si, že se zeptáš zkušené kolegyně, jak napsat e-mail zákaznici, která si stěžuje na zpožděnou zásilku. Kolegyně nepostupuje podle pevného návodu. Vybaví si podobné situace z minulosti a navrhne odpověď, která sedí na tvůj případ.

*Umělá inteligence* (anglicky *artificial intelligence*, zkráceně *AI*) funguje podobně. Je to počítačový systém, který se nenaučil pevná pravidla, ale trénoval na obrovském množství dat – textech, kódu, obrázcích. Naučil se z nich rozpoznávat vzory a vytvářet smysluplné odpovědi.

Všimni si rozdílu oproti programu s nákupem. Ten se řídí pravidly, která jsi mu přesně napsal(a). AI pravidla nikdo nenapsal – "vyčetla" je z příkladů.

### Jazykové modely a nástroje

S jakou AI budeme pracovat my? Se *velkými jazykovými modely* (anglicky *large language model*, zkráceně *LLM*). Zadáš jim úkol v přirozeném jazyce a odpoví textem nebo kódem.

Je dobré rozlišovat **model** a **nástroj**. Model je "mozek", který přemýšlí a generuje text. Nástroj je aplikace kolem něj: okno chatu, editor nebo terminál. Například ChatGPT i Codex od OpenAI používají modely GPT, Claude a Claude Code od Anthropicu používají modely Claude. Proto se může stát, že stejný nástroj po aktualizaci "myslí" jinak – přešel na novější model.

### Co LLM umí a co ne

LLM odpověď *odhaduje* podle vzorů – nic nepočítá ani neověřuje. Proto může znít jistě, a přitom se mýlit. A na rozdíl od deterministického programu z kapitoly o programové logice ti na stejnou otázku může pokaždé odpovědět jinak. Například si vymyslí funkci, která v Pythonu neexistuje, nebo bez upozornění sečte koruny s eury.

Model si také pamatuje jen omezené množství textu. Ve velmi dlouhé konverzaci začne zapomínat, co bylo na začátku, a plete se. S tím se naučíš pracovat v pozdějších lekcích.

Pro tebe z toho plyne jednoduché pravidlo: **co AI napíše, je návrh, ne hotová pravda.** Výsledek vždy ověř – spuštěním, otestováním nebo porovnáním se svým postupem.

### Starý způsob: AI v chatu

Ještě nedávno vypadala práce s AI při programování takhle:

1. Napíšeš do chatu (ChatGPT, Claude) popis toho, co potřebuješ.
2. Zkopíruješ výsledný kód a vložíš ho do editoru.
3. Spustíš ho. Když se objeví chyba, zkopíruješ ji zpátky do chatu.
4. Zkopíruješ opravený kód do editoru a spustíš znovu.
5. Opakuješ, dokud program nefunguje.

Tenhle postup funguje, ale má dvě nevýhody. AI v chatu nevidí tvůj projekt – zná jen to, co jí sám(a) pošleš. Snadno ti tak dá kód, který je sám o sobě správný, ale do projektu nezapadá. A čeká tě spousta ručního kopírování tam a zpátky.

Jedna věc ale fungovala dobře: **měl(a) jsi kontrolu.** Každý kus kódu jsi viděl(a) dřív, než se dostal do projektu.

### Vibe coding

> **Kdy se to hodí:** Napíšeš "udělej mi aplikaci na evidenci výdajů" a za pár minut ji máš. Funguje – ale netušíš, jak, a když se něco rozbije, nevíš, kde hledat.

*Vibe coding* odstraňuje kopírování: AI sama píše kód přímo do projektu, spouští ho, čte výstupy a opravuje chyby. Ty jen popisuješ, co chceš, a výsledek posuzuješ podle toho, jestli "funguje". Do kódu se přitom skoro nedíváš – řídíš se pocitem (*vibe*), že to vypadá dobře.

Výhody jsou lákavé:

- **Rychlost** – od nápadu k první verzi aplikace se dostaneš za pár minut.
- **Méně ruční práce** – žádné kopírování ani přepínání oken.
- **Nízké vstupní nároky** – nemusíš znát syntaxi jazyka.

Má to ale svou cenu:

- **Ztráta přehledu.** AI změní desítky souborů a ty přestaneš vědět, co aplikace vlastně dělá.
- **Bezpečnostní mezery.** AI může nevhodně zacházet s hesly nebo osobními daty a bez kontroly to nepoznáš.
- **Kód, který "jen funguje".** Řešení dělá, co má, ale může být zbytečně pomalé nebo složité na další úpravy.
- **Zbytečné funkce.** Přidat novou funkci je tak snadné, že se zapomíná na otázku, jestli ji vůbec někdo potřebuje.

Vibe coding se hodí na rychlé pokusy a prototypy, které zahodíš. Na aplikaci, kterou chceš dlouhodobě rozvíjet a které chceš věřit, potřebuješ víc.

### AI agent

> **Kdy se to hodí:** Chceš do aplikace s výdaji přidat přepočet z dolarů. Agent si nejdřív projde projekt a navrhne plán. Ty plán schválíš, agent změnu naprogramuje a otestuje a ty si přečteš, co změnil, než ji uložíš.

*AI agent* je jazykový model, který nejen odpovídá, ale také *jedná*. Umí číst soubory v projektu, psát a upravovat kód, spouštět příkazy v terminálu a podle výsledku se rozhodnout, co udělá dál. Pracuje v krocích: něco zkusí, podívá se na výsledek a pokračuje.

V kurzu budeme používat agenta **Codex** od OpenAI, alternativou je **Claude Code** od Anthropicu. Oba můžeš používat v terminálu i v desktopové aplikaci a oba si před důležitými akcemi (třeba úpravou souborů nebo spuštěním příkazu) umí říct o tvé svolení. Jak to nastavit, uvidíš v další části.

### Agentní programování

*Agentní programování* (anglicky *agentic coding*) používá stejné nástroje jako vibe coding, ale s jiným přístupem: **práci řídíš ty**. Agent je tvůj parťák – navrhuje, vysvětluje, píše a testuje. Ty rozhoduješ, co se postaví, kontroluješ výsledek a rozumíš tomu, co vzniklo.

V praxi se držíme postupu, ke kterému se budeme v kurzu stále vracet:

1. **Prozkoumej** – agent si nejdřív přečte projekt a zjistí, jak funguje.
2. **Naplánuj** – agent navrhne postup, ty ho zkontroluješ a případně upravíš.
3. **Naprogramuj** – agent napíše kód podle schváleného plánu.
4. **Otestuj** – ověříš, že program dělá, co má, a že se nic nerozbilo.
5. **Ulož** – změnu si uložíš, aby ses k ní mohl(a) kdykoli vrátit.

Všimni si, že psaní kódu je jen jeden krok z pěti. Ve zbylých čtyřech hraješ hlavní roli ty a právě v nich se uplatní programová logika z druhé kapitoly.

### Tři způsoby práce s AI vedle sebe

| | AI v chatu | Vibe coding | Agentní programování |
|---|---|---|---|
| Vidí AI tvůj projekt? | ne | ano | ano |
| Kdo píše kód do souborů? | ty (kopírováním) | AI | AI |
| Kdo řídí práci? | ty | AI | ty |
| Čteš a ověřuješ výsledek? | ano | málokdy | vždy |

Rozdíl mezi vibe codingem a agentním programováním tedy není v nástroji, ale v tom, kdo práci řídí a jestli rozumíš výsledku. Proto se v kurzu učíme Python – ne abys všechno psal(a) sám(a), ale abys poznal(a), co agent postavil, a uměl(a) to opravit.

### Jak začít: nejdřív plán, potom kód

Nejjednodušší způsob, jak z vibe codingu udělat agentní programování, je nenechat agenta hned psát kód. Požádej ho nejdřív o plán.

Prompt pro agenta:

```text
Chci program v Pythonu, který sečte ceny mého nákupu v Kč a v EUR.
Kód zatím nepiš. Nejdřív mi popiš kroky, které bude program dělat,
a zeptej se mě, pokud ti něco v zadání chybí.
```

Odpověď porovnej s pseudokódem z kapitoly o programové logice. Zeptal se agent, jaký kurz má použít? Pokud ne a kurz si sám zvolil, doplň mu ho do zadání – přesně takhle vypadá spolupráce, ve které práci řídíš ty.

### Cvičení: Plán, nebo rovnou kód?

Zadej výše uvedený prompt do ChatGPT (nebo Claude). Pak v nové konverzaci zkus druhý prompt: "Napiš mi v Pythonu program, který sečte ceny mého nákupu." Porovnej obě odpovědi.

```exercise
id: plan-vs-kod
revision: 1
title: Plán, nebo rovnou kód?
fields:
  - id: rozdil
    label: Čím se odpovědi lišily?
  - id: kontrola
    label: Co jsi v kódu zkontroloval(a)
    guidance: Odpovídají kroky pseudokódu z kapitoly o programové logice? Chybí něco, nebo je tam něco navíc?
  - id: reflexe
    label: Který přístup by sis vybral(a) pro vlastní aplikaci a proč?
```
