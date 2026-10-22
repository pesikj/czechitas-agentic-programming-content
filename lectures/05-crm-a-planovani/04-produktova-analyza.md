---
id: produktova-analyza
title: Produktová analýza
---

# Produktová analýza: co vlastně stavět

S agentem postavíš první verzi CRM za odpoledne. Právě proto je potřeba se nejdřív zastavit a rozhodnout, *co* stavět. Když je stavění rychlé a levné, nejdražší chybou je postavit něco, co nikdo nepotřebuje.

## Produktové řízení

> **Kdy se to hodí:** Agentovi napíšeš "Udělej mi CRM". Dostaneš aplikaci s kalendářem, e-mailovou schránkou a grafy prodejů. Obchodníci ale potřebovali hlavně vědět, komu mají zítra zavolat, a to v aplikaci není.

*Produktové řízení* (anglicky *product management*) je rozhodování o tom, **co stavět, proč a jak poznat, že výsledek někomu pomáhá**. Není to programování ani řízení lidí. Vývoj odpovídá na otázku "jak to postavíme?". Produktové řízení odpovídá na otázky předtím a potom: "má to smysl?", "pro koho to je?" a "jak poznáme, že to funguje?".

Když se software stavěl pomalu a draze, produktové řízení hlídalo hlavně drahé hodiny programátorů. S agentem je první verze levná, a tak se vzácným zdrojem stává něco jiného: pozornost uživatelů, jednoduchost aplikace a tvoje schopnost udržovat kód, který jsi nepsal(a) sám(a).

### Čtyři rizika

Každý produktový nápad nese čtyři rizika:

- **Riziko hodnoty** – budou to lidé skutečně používat? Budou obchodníci Webovky zapisovat obchody do CRM, nebo zůstanou u své tabulky?
- **Riziko použitelnosti** – pochopí, jak se to ovládá?
- **Riziko proveditelnosti** – dokážeme to postavit?
- **Riziko životaschopnosti** – vyplatí se to z hlediska času, nákladů a údržby?

Agent výrazně snižuje hlavně riziko proveditelnosti. Ostatní rizika tím vyniknou: to, že něco jde rychle postavit, neznamená, že to někdo potřebuje, pochopí nebo že se to vyplatí udržovat.

### Dvě role, které střídáš

V malém projektu nemáš produktového manažera a vývojový tým. Všechno jsi ty, a tak střídáš dvě role. **Vývojářská role** se ptá "dokážeme to postavit a jak?". **Produktová role** se ptá "máme to vůbec stavět? Pro koho? Co se stane, když to nepostavíme?".

AI je ochotná a rychlá a nikdy neřekne "počkej, má to smysl?". Proto si odděl **režim rozhodování** (ujasníš si problém, uživatele, úspěch a hranice) od **režimu stavění** (zadáváš práci agentovi). Když režimy splynou, snadno během hodiny přidáš tři funkce a neověříš, jestli první z nich měla smysl. Tahle část je celá v režimu rozhodování.

AI ti může navrhovat možnosti, ale nemá za tebe rozhodovat. Nezná obchodníky Webovky, jejich zvyky ani to, co je štve. Je to velmi rychlý pár rukou, ne člověk, který rozhoduje, kam ty ruce položit.

Pro CRM projdeš čtyři kroky: pochopíš problém a obchodní proces, prozkoumáš existující produkty, rozhodneš, co postavit, a stanovíš, jak poznáš úspěch.

## Krok 1: Pochop problém

> **Kdy se to hodí:** Majitelka Webovky chce CRM, ale když se jí zeptáš, co přesně má evidovat, odpoví "no, ty zákazníky". Dokud nevíš, jak firma prodává a co jí nefunguje, nevíš ani, co má CRM umět.

Nejčastější chyba je začít řešením místo problému: "CRM musí mít grafy prodejů." Lepší otázka zní: "Jaký problém obchodníci teď nedokážou vyřešit?" Pomáhá při tom pohled zvaný *Jobs To Be Done* (česky zhruba "práce, kterou je potřeba udělat"): lidé si produkt "najímají", aby udělali nějaký pokrok. Obchodníci Webovky nechtějí CRM jako takové. Chtějí, aby jim žádný rozjednaný obchod neusnul.

Skutečné problémy najdeš hlavně v rozhovorech s budoucími uživateli. Neptej se "líbila by se vám tahle funkce?", na to lidé snadno řeknou ano. Ptej se na poslední konkrétní zkušenost: "Kdy vám naposledy utekl obchod? Co se stalo? Jak jste to zjistili?" Pro Webovku víme, že obchodníci mají kontakty v e-mailech, rozjednané zakázky v tabulce v Excelu a stav jednání v hlavě. Když někdo onemocní, nikdo neví, komu se má ozvat.

CRM nemá smysl navrhovat od funkcí. Nejdřív musíš pochopit, jakou práci má podporovat. *Obchodní proces* (anglicky *sales process*) je posloupnost kroků, kterými firma prochází od prvního kontaktu s možným zákazníkem až po uzavření obchodu. Každá firma ho má, i když ho nikdy nesepsala.

Nech si s popisem pomoct od AI v obyčejném chatu (ChatGPT nebo Claude). Zatím nic neprogramuješ.

Prompt pro AI:

```text
Pomoz mi popsat obchodní proces malé firmy Webovka s.r.o., která dělá
weby pro jiné firmy. Má tři obchodníky. Zákazníky získává hlavně
z doporučení a z poptávek přes web.

Popiš fáze procesu od prvního kontaktu po uzavření obchodu. U každé fáze
uveď: co se v ní děje, kdo co dělá, jaké informace se při tom zjistí
a kdy fáze končí. Nic si nevymýšlej. Když ti něco chybí, zeptej se mě.
```

Výsledek si zkontroluj a uprav. Pro Webovku vyšel takhle:

| Fáze | Co se děje | Kdy končí |
|---|---|---|
| Vyhledávání | Obchodník najde firmu, která by mohla web potřebovat, nebo přijde poptávka. | Firma projeví zájem o schůzku. |
| Analýza | Na schůzce obchodník zjistí, co firma potřebuje, kolik může zaplatit a kdo rozhoduje. | Je jasné, co firma chce. |
| Nabídka | Obchodník pošle nabídku s cenou a termínem. | Zákazník na nabídku reaguje. |
| Vyjednávání | Ladí se cena, rozsah a podmínky. | Zákazník souhlasí, nebo odmítne. |
| Uzavřeno – získáno / ztraceno | Podepsaná smlouva, nebo odmítnutí. U ztraceného obchodu si zapíšeš důvod. | – |

Z tabulky rovnou vyplývá, co má CRM evidovat: *obchodní případ* (jeden rozjednaný obchod) prochází těmito fázemi a patří k nějaké *firmě*. U firmy navíc sledujeme, jak daleko je od toho, aby u nás nakupovala: nová, lead (projevila zájem), příležitost, aktivní zákazník, bývalý zákazník, neaktivní.

## Krok 2: Prozkoumej existující produkty

> **Kdy se to hodí:** Než vymyslíš vlastní CRM, chceš vědět, co umějí ta, která už existují, co na nich uživatelé chválí a co je štve. Nemusíš vymýšlet všechno znovu a můžeš se vyhnout chybám ostatních.

CRM systémů existují stovky, třeba [Pipedrive](https://www.pipedrive.com), [HubSpot CRM](https://www.hubspot.com/products/crm) nebo český [Raynet](https://raynet.cz). Recenze, diskuse a fóra podpory jsou plná skutečných frustrací popsaných jazykem uživatelů. Ručně je procházet by ale trvalo dny. Tady pomůže *deep research* (hloubkový průzkum): režim AI, který sám prochází desítky aktuálních webových stránek, recenzí a diskusí a sestaví z nich zprávu s odkazy na zdroje. Na rozdíl od běžného chatu nevychází jen z toho, co se AI naučila při tréninku. Průzkum trvá několik minut až desítek minut.

::::alternatives
:::option{label="ChatGPT"}
Napiš do pole pro zprávu `@Deepresearch` a za něj zadání. (Deep research najdeš i v nabídce nástrojů pod tlačítkem **+**.) ChatGPT nejdřív navrhne plán průzkumu, který můžeš upravit, a pak se pustí do hledání.
:::
:::option{label="Claude"}
V poli pro zprávu zapni **Research** a napiš zadání.
:::
::::

Prompt pro AI:

```text
Porovnej CRM systémy vhodné pro malou firmu se 3 obchodníky, která dělá
weby pro jiné firmy: Pipedrive, HubSpot CRM, Raynet a Zoho CRM.

1. Jaké funkce mají všechny a uživatelé je považují za základ?
2. Které funkce uživatelé v recenzích nejvíc chválí a co je nejvíc štve?
3. Co z toho je důležité pro malou firmu a co je zbytečně složité?

Výsledek shrň do tabulky funkcí. U každého tvrzení uveď zdroj.
```

Zprávu čti kriticky. Klikni aspoň na dva tři zdroje a ověř, že opravdu říkají to, co z nich AI vyvodila. AI se umí splést i s odkazem na zdroj. Hledej hlavně opakující se vzory: funkce, které mají všechny systémy, jsou základní očekávání. Stížnosti, které se opakují v recenzích, jsou místa, kde se můžeš odlišit.

Nezapomeň ani na konkurenci, která není aplikace. Pro Webovku je největším soupeřem CRM tabulka v Excelu, kterou obchodníci znají a které věří. Nové CRM musí být v něčem jednodušší nebo lepší, jinak se k ní vrátí.

## Krok 3: Rozhodni, co postavit

Teď máš popsaný problém i proces a víš, co umějí ostatní. Zbývá rozhodnout, co postavíš jako první. Funkcí, které by se hodily, bude vždycky víc než času. Produktová role se snaží o tři věci: **postavit správnou věc** (řešit skutečný problém skutečného člověka), **neplýtvat úsilím** (nestavět, co nikdo nepotřebuje) a **průběžně se učit** (brát každou funkci jako otázku, ne jako hotový fakt).

**Vize** je jedna nebo dvě věty o tom, pro koho produkt je a co mu přinese. Pro Webovku: "Obchodníci Webovky mají na jednom místě přehled o všech firmách a rozjednaných obchodech, takže žádný obchod neusne jen proto, že na něj někdo zapomněl."

**Strategie** je zvolená cesta k vizi: kteří uživatelé jsou první, který problém řešíš jako první a co zatím záměrně neděláš. Pro Webovku: první jsou tři obchodníci, první problém je přehled rozjednaných obchodů, a dokud aplikace běží na jednom počítači, neřešíme přihlašování ani spolupráci na dálku.

**Roadmapa** je přehled toho, na čem budeš pracovat. Pro malý projekt stačí rozdělení **Teď / Další / Později**. Roadmapa bez vize a strategie je jen seznam úkolů, a ten se snadno zaplní prací, která dohromady netvoří žádný produkt.

| Teď (první verze) | Další | Později |
|---|---|---|
| Firmy se stavem | Kontakty (lidé z firem) | Nasazení na internet a sdílení dat mezi obchodníky |
| Obchodní případy s fází a hodnotou | Úpravy a mazání záznamů | Přihlášení uživatelů |
| Seznamy a formuláře pro přidání | Součet hodnoty otevřených obchodů | Napojení na e-mail a kalendář |

Než se funkce dostane na roadmapu, měla by přežít čtyři otázky:

- Čí problém řeší a jak silně ho ten člověk cítí?
- Je to skutečný problém, nebo jen náš nápad?
- Zapadá to do vize?
- Co bude stát nejen vytvoření, ale i dlouhodobá údržba?

**Prioritizace.** Nejjednodušší nástroj je otázka *hodnota vs. úsilí*: přednost mají věci s vysokou hodnotou a nízkým úsilím. U práce s agentem do úsilí počítej i údržbu, ladění a budoucí změny: funkce, kterou agent napíše za deset minut, ale ty ji pak měsíc opravuješ, levná není. Existují i formálnější metody, třeba *RICE* (skóre podle dosahu, dopadu, jistoty a úsilí) nebo *Kano model* (rozlišuje základní očekávání a příjemná překvapení). Pro malý projekt si stačí pamatovat princip: nejdřív postav základní očekávání (bez evidence obchodů CRM nemá smysl), teprve potom efektní doplňky.

**Co nestavět.** Nejtěžší produktové rozhodnutí je říct ne. Produkt není hromada funkcí, ale soubor rozhodnutí, která spolu dávají smysl. Každá funkce, kterou do první verze nepřidáš, je kód, který nemusíš kontrolovat a udržovat, a obrazovka, kterou nemusíš obchodníkům vysvětlovat. Otázka "co odebrat?" je stejně důležitá jako "co přidat?", jen se pokládá mnohem méně často.

**Kdy je hotovo.** Protože stavění je rychlé, dá se nekonečně vylepšovat. Předem si urči, co znamená "hotovo". Pro první verzi CRM: obchodník přidá firmu i obchodní případ a uvidí je v seznamu. "Dost dobré k vyzkoušení s obchodníky" je lepší cíl než "dokonalé".

## Krok 4: Jak poznáš, že to funguje

**Metriku úspěchu si stanov před stavěním,** ne až potom. Pro Webovku: "Po měsíci jsou v CRM všechny rozjednané obchody a obchodníci už nepoužívají svou tabulku v Excelu." Když metriku hledáš až po vydání, snadno si najdeš číslo, které potvrdí, co chceš slyšet. Předem stanovená hranice tě drží poctivěji.

Měřit jde jen to, co zaznamenáváš. U CRM je to snadné: počet obchodních případů a datum jejich vytvoření jsou přímo v databázi. Z lekce 03 už víš, že program může důležité události zapisovat i do logu.

Po vyzkoušení má každá funkce tři možné výsledky: **ponechat** (splnila hranici), **upravit** (je vidět, že pomáhá, ale něco nefunguje dobře) nebo **zrušit** (nikdo ji nepoužívá). Zrušení není selhání. Je to levný pokus, který přinesl pravdivou odpověď.

Špatný návyk se jmenuje *feature factory* (továrna na funkce): vymyslet, postavit, vydat, další funkce, pořád dokola a bez učení. Lepší je smyčka:

1. **Rozhodni** – vyber problém nebo funkci a stanov metriku úspěchu.
2. **Postav** – nech agenta funkci postavit.
3. **Otestuj** – ověř, že funguje podle zadání.
4. **Změř** – sleduj, jestli ji obchodníci opravdu používají.
5. **Pouč se** – funkci ponech, uprav, nebo zruš. Další rozhodnutí může být i odebrání funkce.

## PM Skills

S rozhodováním ti pomůže AI s pluginy PM Skills, které sis nainstaloval(a) v přípravě na lekci. Každý plugin se hodí na jinou část analýzy.

**pm-product-discovery** hledá řešení, prověřuje předpoklady a připravuje rozhovory s uživateli. Například:

```text
Pomocí pm-product-discovery připrav krátký scénář rozhovoru se třemi
obchodníky firmy Webovka s.r.o. Chci zjistit, jak dnes evidují firmy
a rozjednané obchody, co jim nefunguje a jaké náhradní postupy používají.
Ptej se na konkrétní minulé zkušenosti.
```

**pm-product-strategy** ujasňuje vizi, cílovou skupinu a odlišení od konkurence. Například:

```text
Pomocí pm-product-strategy mi pomoz vysvětlit, proč by obchodníci Webovky
měli přejít z tabulky v Excelu na naše CRM. Navrhni hlavní přínos
a označ tvrzení, která ještě musím ověřit.
```

**pm-execution** sestaví roadmapu, seřadí priority a připraví zadání funkcí. Projdi s ním krok 3. Vlož mu popis obchodního procesu z kroku 1 a shrnutí průzkumu z kroku 2.

Prompt pro AI:

```text
Pomocí pm-product-strategy a pm-execution mi pomoz rozhodnout, co má umět
první verze CRM pro firmu Webovka s.r.o. Obchodní proces a výsledky průzkumu
existujících CRM jsou níže.

Navrhni vizi v jedné větě, roadmapu Teď / Další / Později a metriku úspěchu
první verze. První verze poběží jen na mém počítači a bude bez přihlašování.
U každé funkce vysvětli, proč patří tam, kam patří.
Než začneš, zeptej se mě na to, co ti chybí.

[sem vlož popis obchodního procesu a shrnutí průzkumu]
```

Výsledek porovnej s roadmapou výše. Liší se? Je to proto, že AI našla něco, na co jsi nemyslel(a), nebo proto, že nezná tvou firmu? AI může navrhovat možnosti, ale rozhodnutí je tvoje.

Výsledkem produktové analýzy je jasná představa o první verzi CRM. V další části ji předáš agentovi v brainstormingu a on z ní sepíše návrh aplikace.

## Cvičení: Produktová analýza vlastního projektu

Během kurzu budeš kromě CRM stavět i vlastní aplikaci. Část cvičení v dalších lekcích bude věnovaná právě jí. Dnes pro ni uděláš stejnou analýzu jako pro Webovku a na konci budeš mít podnikatelský záměr v malém: víš, pro koho aplikace je, co bude umět jako první a jak poznáš, že se povedla.

**Nemáš nápad?** Vyber si problém, který řešíš ty nebo někdo z tvého okolí. Pro inspiraci: rezervace termínů pro kadeřnici nebo fyzioterapeuta, evidence výpůjček knih a nářadí mezi sousedy, plánování jídel a nákupů na týden, přehled tréninků a docházky v malém sportovním klubu, evidence zakázek a faktur pro OSVČ. Drž se aplikace, kterou zvládneš postavit za několik týdnů: jedna skupina uživatelů a dvě tři hlavní věci, které eviduje.

Postupuj stejně jako u CRM. Kroky 1, 3 a 4 dělej v obyčejném chatu s PM Skills, krok 2 v deep research.

**1. Pochop problém.** "Aplikace na sport" je nápad, se kterým agent nic nepostaví. Popiš konkrétního uživatele, jeho problém a jak ho řeší dnes.

Prompt pro AI:

```text
Pomocí pm-product-discovery mi pomoz zpřesnit nápad na aplikaci:
[jedna až dvě věty o nápadu].
Ptej se mě postupně, po jedné otázce: kdo přesně bude aplikaci používat,
jaký problém mu řeší, jak ho řeší dnes a co ho na tom štve, v jaké
situaci aplikaci otevře a co v ní udělá. Ptej se na konkrétní minulé
zkušenosti. Nic si nevymýšlej. Na konci shrň nápad do pěti vět.
```

Shrnutí si zkontroluj. Odpovídá tomu, co chceš postavit? Pokud ne, oprav ho. Když můžeš, zeptej se na stejné otázky aspoň jednoho budoucího uživatele.

**2. Zmapuj konkurenci.** Pusť deep research na existující aplikace, které řeší stejný problém. Nezapomeň ani na konkurenci bez aplikace: tabulku v Excelu, papírový diář nebo skupinu na WhatsAppu.

Prompt pro AI:

```text
Najdi existující aplikace a jiná řešení (třeba tabulky nebo papír)
pro tento problém: [shrnutí nápadu z kroku 1].

1. Jaké funkce mají všechna řešení a uživatelé je považují za základ?
2. Co uživatelé v recenzích chválí a co je nejvíc štve?
3. Kolik stojí a pro koho jsou určená?
4. Co by moje aplikace mohla dělat jinak nebo lépe?

Výsledek shrň do tabulky. U každého tvrzení uveď zdroj.
```

Ověř aspoň dva tři zdroje. Když zjistíš, že přesně tvoje aplikace už existuje a je zdarma, nevadí: pro učení ji postavit můžeš, jen si ujasni, čím by se tvoje verze lišila.

**3. Vize, roadmapa a priority.** S PM Skills sestav vizi, strategii, roadmapu Teď / Další / Později a definici "hotovo" pro první verzi.

Prompt pro AI:

```text
Pomocí pm-product-strategy a pm-execution mi pomoz rozhodnout, co má umět
první verze mé aplikace. Nápad a výsledky průzkumu jsou níže.

Navrhni vizi v jedné větě, strategii (první uživatelé, první problém,
co zatím nedělám) a roadmapu Teď / Další / Později. Funkce seřaď podle
hodnoty a úsilí. První verze poběží jen na mém počítači, bez přihlašování,
a musím ji s AI agentem postavit za několik týdnů jako začátečník(ce)
v Pythonu a Djangu. U každé funkce vysvětli, proč patří tam, kam patří.
Napiš i, co do první verze záměrně nepatří.
Než začneš, zeptej se mě na to, co ti chybí.

[sem vlož shrnutí nápadu a shrnutí průzkumu]
```

Roadmapu po AI uprav. Sloupec Teď by měl mít nejvýš tři čtyři položky, podobně jako u CRM. Když je delší, přesuň zbytek do Další.

**4. Úspěch a podnikatelský pohled.** Stanov metriku úspěchu první verze a odpověz na čtyři otázky, každou jednou dvěma větami:

- **Pro koho a proč:** Kdo aplikaci použije a co tím získá (čas, peníze, přehled)?
- **Proč ne konkurence:** Proč by nepoužil existující řešení z kroku 2?
- **Náklady:** Co tě bude stát vývoj a provoz (tvůj čas, předplatné AI, později hosting)?
- **Životaschopnost:** Kdyby aplikace měla vydělávat, kdo by za ni platil a kolik? Pokud ji stavíš jen pro sebe, napiš to. I to je platná odpověď.

**5. Ulož výsledky.** V Dokumentech vytvoř složku pro projekt (třeba `rezervace`), otevři ji ve VS Code a zapni Git. Vytvoř v ní soubor `produkt.md` a vlož do něj výsledky kroků 1–4. Udělej commit `Produktová analýza` a projekt publikuj na GitHub jako soukromý repozitář. Soubor `produkt.md` použiješ v další části jako podklad pro brainstorming s agentem.

```exercise
id: vlastni-projekt-analyza
revision: 1
title: Produktová analýza vlastního projektu
fields:
  - id: napad
    label: Nápad v pěti větách
    guidance: Kdo aplikaci použije, jaký problém mu řeší a jak ho řeší dnes?
  - id: konkurence
    label: Konkurence
    guidance: Jaká řešení už existují (včetně tabulek a papíru)? Co na nich uživatele štve? Ověřil(a) jsi zdroje?
  - id: roadmapa
    label: Vize, strategie a roadmapa
    guidance: Co je ve sloupci Teď a proč? Co jsi oproti návrhu AI změnil(a)? Co do první verze záměrně nepatří?
  - id: podnikatelsky-pohled
    label: Metrika úspěchu a podnikatelský pohled
    guidance: Jak poznáš, že se první verze povedla? Pro koho a proč, proč ne konkurence, náklady a životaschopnost.
  - id: repozitar
    label: Odkaz na repozitář
    guidance: Je v něm soubor produkt.md? Je repozitář soukromý?
```
