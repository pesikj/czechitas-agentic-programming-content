---
id: brainstorming
title: Brainstorming
---

# Brainstorming: co vlastně stavět

Z produktové analýzy víš, co má první verze CRM umět a proč. Teď to potřebuješ předat agentovi tak, aby to pochopil stejně jako ty. Agent je ale ochotný a rychlý a sám nikdy neřekne "počkej, co tím přesně myslíš?". To ho naučí skill **brainstorming** z pluginu Superpowers, který sis nainstaloval(a) v přípravě na lekci.

## Proč nejdřív brainstorming

> **Kdy se to hodí:** Agentovi pošleš roadmapu z produktové analýzy a napíšeš "postav to". Agent si sám rozhodne, jestli může firma existovat bez IČO, jestli jde obchodní případ uložit bez hodnoty a jak budou vypadat formuláře. Že to rozhodl jinak, než bys chtěl(a), zjistíš až v hotové aplikaci.

Agent si zadání vždycky nějak domyslí. Když mu řekneš málo, rozhodne za tebe stovky drobností a ty zjistíš, že je rozhodl jinak, až v hotovém kódu. *Brainstorming* je rozhovor, ve kterém se tě agent nejdřív vyptá, co a proč chceš postavit, a teprve pak sepíše návrh. Je to jako schůzka s architektkou: než nakreslí dům, zeptá se, kolik vás v něm bude bydlet a jestli vaříte.

Skill má jedno pevné pravidlo: **dokud návrh neschválíš, agent nic nestaví.** Nevytvoří projekt, nenainstaluje balíček ani nenapíše řádek kódu. Smí jen číst a ptát se.

## Jak brainstorming probíhá

1. **Agent nabídne, že otázky můžeš přeskočit.** Když napíšeš, že chceš rovnou začít, brainstorming skončí. U CRM to nedělej.
2. **Ptá se po jedné otázce.** Každá zpráva končí jednou otázkou, často na konkrétní situaci: "Popiš mi, kdy naposledy obchodníkům chyběl přehled." Odpovídej vlastními slovy. Když nevíš, napiš "navrhni něco" a agent přijde s konkrétním návrhem.
3. **Průběžně shrnuje.** Jakmile jedné části rozumí, popíše ji vlastními slovy a zeptá se, co je špatně nebo co chybí. Co si jen domýšlí, označí jako odhad. Tady opravuj, dokud shrnutí nesedí.
4. **Může ti něco ukázat.** U obrazovek a formulářů ti agent může nabídnout, že otevře v prohlížeči náhled, jak by aplikace mohla vypadat. Nabídku klidně přijmi.
5. **Odhadne velikost práce.** U drobné změny se domluvíte v chatu. U celé aplikace řekne, že sepíše návrh.
6. **Sepíše návrh.** Návrh je dokument v projektu, ve složce `docs/superpowers/specs/`, třeba `docs/superpowers/specs/2026-10-22-crm-design.md`. Agent ho rovnou uloží commitem. Než ti ho předá, přečte ho pomocný agent v roli programátora, který by podle něj měl stavět. Když mu něco chybí, agent se tě ještě jednou zeptá.
7. **Návrh schválíš.** Až teď se může začít plánovat.

## Podklady od Webovky

V lekci budeš hrát majitelku nebo majitele firmy, pro kterou se CRM staví. Agent se tě bude ptát a ty odpovídáš podle těchto podkladů. Je to shrnutí produktové analýzy z minulé části. Pokud ti v ní vyšlo něco jiného, odpovídej podle své verze. Podklady nemusíš vkládat najednou. Odpovídej na to, na co se ptá.

**Firma.** Webovka s.r.o. dělá weby pro jiné firmy. Má tři obchodníky. Zákazníky získává hlavně z doporučení a z poptávek přes web. Kontakty mají obchodníci v e-mailech, rozjednané zakázky v tabulce v Excelu a stav jednání v hlavě. Když někdo onemocní, nikdo neví, komu se má ozvat.

**Obchodní proces.** Ve Webovce vypadá takhle:

| Fáze | Co se děje | Kdy končí |
|---|---|---|
| Vyhledávání | Obchodník najde firmu, která by mohla web potřebovat, nebo přijde poptávka. | Firma projeví zájem o schůzku. |
| Analýza | Na schůzce obchodník zjistí, co firma potřebuje, kolik může zaplatit a kdo rozhoduje. | Je jasné, co firma chce. |
| Nabídka | Obchodník pošle nabídku s cenou a termínem. | Zákazník na nabídku reaguje. |
| Vyjednávání | Ladí se cena, rozsah a podmínky. | Zákazník souhlasí, nebo odmítne. |
| Uzavřeno – získáno / ztraceno | Podepsaná smlouva, nebo odmítnutí. | – |

**Vize.** Obchodníci Webovky mají na jednom místě přehled o všech firmách a rozjednaných obchodech, takže žádný obchod neusne jen proto, že na něj někdo zapomněl.

**Co má první verze umět (sloupec Teď).** Evidovat firmy (název, IČO, e-mail, telefon a stav: nová, lead, příležitost, aktivní zákazník, bývalý zákazník, neaktivní) a obchodní případy (firma, popis, hodnota v Kč a fáze podle tabulky). Seznamy obojího a formuláře pro přidání.

**Co zatím ne (sloupce Další a Později).** Přihlašování, nasazení na internet, napojení na e-mail a kalendář, úpravy a mazání záznamů. Aplikace poběží jen na jednom počítači.

**Jak poznáš, že se povedla.** Po měsíci jsou v CRM všechny rozjednané obchody a obchodníci už nepoužívají svou tabulku v Excelu.

**Jak se postaví.** V Pythonu pomocí Djanga, projekt spravuje uv, data se ukládají do databáze SQLite. Kód má být co nejjednodušší, protože mu musí rozumět začátečník.

## Brainstorming CRM

V Dokumentech vytvoř složku `crm`, otevři ji ve VS Code a zapni v ní Git (**Initialize Repository** v panelu Source Control). Agent do projektu uloží návrh commitem, proto musí být projekt repozitář od začátku.

Spusť agenta v terminálu ve VS Code a pošli mu zadání. Agent by měl brainstorming použít sám, jistější ale je napsat mu to.

Prompt pro agenta:

```text
Použij skill brainstorming. Chci postavit jednoduchou CRM aplikaci pro
malou firmu Webovka s.r.o., která dělá weby pro jiné firmy.
Postav ji v Pythonu pomocí Djanga, projekt spravuj nástrojem uv
a data ukládej do databáze SQLite. Jsem začátečník(ce), kód piš
co nejjednodušší. Zeptej se mě na všechno, co potřebuješ vědět.
```

Zadání říká, *z čeho* se má aplikace postavit, ale skoro nic o tom, *co* má umět. To nech na rozhovoru. Na otázky odpovídej podle podkladů od Webovky. Když se agent zeptá na něco, co v podkladech není (třeba "Mají obchodníci vidět i obchody kolegů?"), rozhodni se sám(a). Takové otázky jsou přesně místa, kde by se jinak agent rozhodl za tebe.

Rozhovor trvá obvykle 10–20 minut. Když se ti zdá, že se agent ptá na zbytečnosti, napiš mu to. Když ti nabídne, že rovnou postaví rychlou zkušební verzi (*spike*), odmítni: dnes chceš nejdřív návrh a plán.

## Jak návrh číst

Až agent návrh předá, otevři ho ve VS Code (`docs/superpowers/specs/...-design.md`) a přečti ho celý. Ptej se:

- **Odpovídá podkladům?** Jsou tam obě evidence, všechny údaje, stavy i fáze? Nepřidal agent něco, o co jsi nežádal(a)?
- **Co nepatří do první verze?** Dobrý návrh má i seznam toho, co se stavět *nebude* (anglicky *non-goals*). Jsou tam přihlašování, nasazení a e-mail?
- **Co rozhodl agent sám?** Agent u návrhu vypíše rozhodnutí, která udělal za tebe, třeba "IČO beru jako text o 8 znacích bez kontroly platnosti". Souhlasíš s nimi?
- **Je to celé?** Mohl by podle návrhu někdo stavět, aniž by se tě na cokoli ptal?

Když chceš něco změnit, napiš to agentovi, třeba "E-mail a telefon nech nepovinné." Agent návrh upraví a uloží. Teprve až s návrhem souhlasíš celým, napiš to výslovně:

```text
Návrh jsem přečetl(a) a schvaluji ho.
```

"Zní to dobře" k návrhu, který jsi nečetl(a), není schválení. Schvaluješ to, co je napsané, ne to, co sis při rozhovoru představoval(a).

V panelu Source Control v sekci **Graph** uvidíš commit s návrhem. Návrh je teď součástí projektu a v další části z něj agent napíše plán.

## Cvičení: Brainstorming vlastního projektu

V minulé části jsi udělal(a) produktovou analýzu vlastního projektu a výsledky uložil(a) do souboru `produkt.md`. Teď je předáš agentovi stejně jako podklady od Webovky a na konci budeš mít schválený návrh, podle kterého se dá stavět.

1. **Otevři projekt.** Otevři ve VS Code složku vlastního projektu, ve které je soubor `produkt.md`.
2. **Brainstorming.** Spusť agenta a pošli mu prompt:

   ```text
   Použij skill brainstorming. Chci postavit aplikaci, kterou popisuje
   soubor produkt.md: najdeš v něm nápad, konkurenci, vizi, roadmapu
   a metriku úspěchu. Postav první verzi podle sloupce Teď. Použij Python
   a Django, projekt spravuj nástrojem uv a data ukládej do databáze SQLite.
   Jsem začátečník(ce), první verze poběží jen na mém počítači a bez
   přihlašování. Zeptej se mě na všechno, co v souboru chybí.
   ```

   Tady odpovídáš za sebe. Když nevíš, jak by to mělo fungovat, napiš "navrhni něco" a návrh posuď.
3. **Přečti a schval návrh.** Projdi ho podle otázek z části "Jak návrh číst". Odpovídá roadmapě v `produkt.md`? Hlídej hlavně, co do první verze *nepatří*: čím kratší seznam funkcí, tím větší šance, že aplikaci dokončíš. Pak návrh výslovně schval.
4. **Odešli na GitHub.** Návrh je uložený commitem. Pošli ho na GitHub tlačítkem **Sync Changes**.

Návrh nech zatím ležet. V dalších lekcích z něj necháš agenta napsat plán a aplikaci postavíš.

```exercise
id: vlastni-projekt-brainstorming
revision: 1
title: Brainstorming vlastního projektu
fields:
  - id: otazky
    label: Na co se agent ptal
    guidance: Která otázka tě nejvíc donutila přemýšlet? Na co jsi odpověď neznal(a)?
  - id: navrh
    label: Co jsi v návrhu změnil(a)
    guidance: Odpovídá návrh roadmapě v produkt.md? Co agent rozhodl za tebe? Co jsi opravil(a)?
  - id: repozitar
    label: Odkaz na repozitář
    guidance: Je v něm vedle produkt.md i návrh ve složce docs/superpowers/specs?
```
