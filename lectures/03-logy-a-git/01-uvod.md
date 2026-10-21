---
id: uvod
title: Úvod
---

# Logy a Git

Minule jsi nechal(a) agenta napsat program `nakup.py`, rozbil(a) ho překlepem v datech a viděl(a), že výjimka umí chybu potichu schovat: program nespadl, ale vypsal špatný součet. Dnes na to navážeme:

1. **Logy** – jak program během práce zapisuje záznam o tom, co dělal, a jak v něm najdeš, co se pokazilo.
2. **Sledování logů s pomocí AI** – jak ti agent pomůže vytáhnout z logu to podstatné, a proč jeho závěr musíš ověřit.
3. **Git ve VS Code** – jak si uložit každou funkční verzi programu, zjistit, co se v kódu změnilo, a vrátit se zpátky, když se úprava nepovede.

**Proč to potřebuješ:** Program, který běží sám (třeba každý večer), nikdo nesleduje. Když se v něm něco pokazí, jedinou stopou je záznam, který po sobě nechal. Bez něj nepoznáš ani to, že je výsledek špatně. Logy navazují na výjimky z minulé lekce: výjimka zabrání pádu, log zajistí, že se o chybě dozvíš. Git řeší druhou stranu téhož problému: když program rozbije změna v kódu, třeba od agenta, ukáže ti, co se změnilo, a vrátí tě k verzi, která fungovala.

**Po lekci budeš umět:**
- Víš, co je log, a znáš úrovně DEBUG, INFO, WARNING, ERROR a CRITICAL.
- Umíš nechat agenta přidat do programu logování a z logu zjistit, co se stalo, u které položky a kdy.
- Umíš nechat AI shrnout log a její závěr ověřit v datech a kódu.
- Umíš ve VS Code zapnout Git, udělat commit a zkontrolovat změny, a víš, proč si uložit funkční verzi dřív, než necháš agenta měnit kód.
- Umíš publikovat projekt na GitHub, připravit novou funkci ve větvi a dostat ji přes pull request a code review do `main`.
