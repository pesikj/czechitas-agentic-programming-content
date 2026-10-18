---
id: logy
title: Logy
---

# Logy: co se stalo, když jsi u toho nebyl(a)

Minule jsi nechal(a) agenta napsat program `nakup.py`, rozbil(a) ho překlepem v datech a viděl(a), že výjimka umí chybu potichu schovat: program nespadl, ale vypsal špatný součet. Dnes na to navážeme:

1. **Logy** – jak program během práce zapisuje záznam o tom, co dělal, a jak v něm najdeš, co se pokazilo.
2. **Sledování logů s pomocí AI** – jak ti agent pomůže vytáhnout z logu to podstatné, a proč jeho závěr musíš ověřit.
3. **Git** – jak si uložit každou funkční verzi programu, zjistit, co se v kódu změnilo, a vrátit se zpátky, když se úprava nepovede.

**Proč to potřebuješ:** Program, který běží sám (třeba každý večer), nikdo nesleduje. Když se v něm něco pokazí, jedinou stopou je záznam, který po sobě nechal. Bez něj nepoznáš ani to, že je výsledek špatně. Logy navazují na výjimky z minulé lekce: výjimka zabrání pádu, log zajistí, že se o chybě dozvíš. Git řeší druhou stranu téhož problému: když program rozbije změna v kódu, třeba od agenta, ukáže ti, co se změnilo, a vrátí tě k verzi, která fungovala.

**Po lekci budeš umět:**
- Víš, co je log, a znáš úrovně DEBUG, INFO, WARNING, ERROR a CRITICAL.
- Umíš nechat agenta přidat do programu logování a zkontrolovat, co zapisuje.
- Umíš z logu zjistit, co se stalo, u které položky a kdy.
- Umíš nechat AI shrnout log a její závěr ověřit v datech a kódu.
- Víš, co je Git, repozitář a commit, a proč si uložit funkční verzi dřív, než necháš agenta měnit kód.
- Víš, co dělají push, pull a clone, k čemu je GitHub a k čemu slouží větve a pull request.

## Logy: záznam o tom, co se stalo

> **Kdy se to hodí:** Program běží každý večer sám a ráno ti pošle součet útraty. Když se v noci něco pokazí, nikdo u toho nebyl. Potřebuješ záznam, ze kterého zjistíš, co se stalo.

*Log* (česky *záznam* nebo *protokol*) je zpráva, kterou program zapisuje během své práce – obvykle do souboru. Každá zpráva má čas, *úroveň závažnosti* a text. Připomíná lodní deník: nezapisuje se do něj kvůli někomu konkrétnímu, ale když se něco stane, víš, kde hledat.

Python má pro logy připravený modul `logging`. Rozlišuje pět základních úrovní:

| Úroveň | Kdy se používá | Příklad v programu s nákupem |
|---|---|---|
| `DEBUG` | podrobnosti pro hledání chyb | "Převádím 45 EUR na Kč" |
| `INFO` | běžný průběh programu | "Načteno 5 položek ze souboru nakup.csv" |
| `WARNING` | něco je podezřelé, ale program pokračuje | "Položka nemá vyplněnou měnu, beru ji jako CZK" |
| `ERROR` | něco se nepovedlo | "Neplatná cena u položky Karimatka: '59O'" |
| `CRITICAL` | program nemůže pokračovat | "Soubor nakup.csv neexistuje" |

Úrovně slouží jako filtr. Při běžném provozu zapisuješ třeba jen `INFO` a vyšší, při hledání chyby zapneš i `DEBUG`.

Vyzkoušíš to na programu s nákupem. V `nakup.csv` znovu udělej u karimatky překlep `59O` z minulé lekce. Pokud máš verzi programu s aktuálním kurzem ze cvičení, budou se částky ve výstupu lišit od ukázek.

Takhle vypadá program s logy. Na začátek přibude nastavení:

```python
import logging

logging.basicConfig(
    filename="nakup.log",
    level=logging.INFO,
    format="%(asctime)s %(levelname)s %(message)s",
    encoding="utf-8",
)
```

Logy se budou zapisovat do souboru `nakup.log`, a to od úrovně `INFO` výš. Každý řádek bude mít čas, úroveň a zprávu.

Ve funkci `cena_v_kc` už výjimka chybu nespolkne, ale zapíše ji:

```python
    except ValueError:
        logging.error("Neplatná cena u položky %s: %r", polozka["polozka"], polozka["cena"])
        return 0
```

Do funkce `nacti_polozky` přibude `logging.info(...)` s počtem načtených položek a na konec programu `logging.info(...)` s výsledkem. Celý kód si můžeš nechat od agenta doplnit promptem "Přidej do nakup.py logování do souboru nakup.log. Chybné ceny zapiš jako ERROR."

Po spuštění s překlepem `59O` je v souboru `nakup.log`:

```text
2026-10-18 15:05:24,937 INFO Načteno 5 položek ze souboru nakup.csv
2026-10-18 15:05:24,937 ERROR Neplatná cena u položky Karimatka: '59O'
2026-10-18 15:05:24,937 INFO Celkem: 3114.00 Kč
```

Výsledek je pořád neúplný, ale tentokrát o tom existuje záznam. Z logu je přesně vidět, která položka chybí, proč a kdy se to stalo. Do logů nikdy nezapisuj hesla, čísla karet ani jiné citlivé údaje – logy si často čte víc lidí a nástrojů, než čekáš.

## Sledování logů s pomocí AI

U malého programu si log přečteš sám(a). Skutečné aplikace ale běží na serverech nepřetržitě a zapisují tisíce řádků denně. Tam se logy *monitorují*: speciální nástroje je sbírají na jedno místo, hledají v nich chyby a pošlou upozornění, když se objeví řádek s úrovní `ERROR` nebo `CRITICAL`.

S logy umí pracovat i AI. Agent si soubor přečte v terminálu stejně jako obsah složky Dokumenty – log je přece jen text. Umí z tisíců řádků vytáhnout to podstatné, najít opakující se chyby a navrhnout jejich příčinu.

Prompt pro agenta:

```text
Přečti soubor nakup.log. Shrň, jaké chyby a varování se objevily,
u kterých položek a co je jejich nejpravděpodobnější příčina.
Nic neopravuj, jen mi to vysvětli.
```

I tady platí, co už znáš: co agent z logu vyvodí, je návrh. Ověř si ho v datech a v kódu, než podle něj začneš něco měnit.

## Cvičení: Tichá chyba

Vrať program do funkční podoby (s opravenými daty) a smaž soubor `nakup.log`. Python do logu nové řádky jen přidává, takže by v něm zůstala chyba z minulého spuštění. Pak v souboru `nakup.csv` změň u spacáku měnu z `EUR` na malé `eur` a program spusť. Spadne? Objeví se něco v logu? Jaký je výsledek a proč? Nakonec požádej agenta, aby program upravil tak, aby se o takové chybě dozvěděl(a), a zkontroluj, co změnil.

```exercise
id: ticha-chyba
revision: 1
title: Tichá chyba
fields:
  - id: vysledek
    label: Co program vypsal a proč
    guidance: Spadl program? Je výsledek správně? Kolik korun ve výsledku chybí a čím to je?
  - id: log
    label: Co bylo v logu
  - id: oprava
    label: Jak chybu opravil agent
    guidance: Co přesně změnil? Dozvíš se teď o podobné chybě? Je to oprava příčiny, nebo jen schování problému?
```
