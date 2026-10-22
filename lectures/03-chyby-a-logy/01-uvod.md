---
id: uvod
title: Úvod
---

# Chyby, balíčky a logy

Minule sis rozmyslel(a) logiku programu na sčítání nákupu, poznal(a) agentní programování a nastavil(a) svého agenta. Dnes ho poprvé necháš napsat skutečný program a naučíš se, co dělat, když selže:

1. **Kód od agenta** – necháš agenta napsat program `nakup.py`, který sečte nákup ze souboru CSV, a naučíš se ho číst včetně funkcí.
2. **Chyby a výjimky** – jak vypadá syntaktická chyba a chyba za běhu, jak přečíst traceback a proč výjimka umí chybu potichu schovat.
3. **Balíčky a uv** – jak do projektu přidat hotový nástroj od jiných lidí a nechat program stáhnout aktuální kurz eura.
4. **Logy** – jak program během práce zapisuje záznam o tom, co dělal, a jak v něm najdeš, co se pokazilo.
5. **Sledování logů s pomocí AI** – jak ti agent pomůže vytáhnout z logu to podstatné, a proč jeho závěr musíš ověřit.

**Proč to potřebuješ:** Chyby se objeví vždycky, i v kódu od agenta. Musíš poznat, co se stalo, a posoudit, jestli je oprava od agenta opravdu oprava, nebo jen chybu schová. Program, který běží sám (třeba každý večer), navíc nikdo nesleduje. Když se v něm něco pokazí, jedinou stopou je záznam, který po sobě nechal: výjimka zabrání pádu, log zajistí, že se o chybě dozvíš.

**Po lekci budeš umět:**
- Umíš nechat agenta napsat program, spustit ho přes `uv run` a zhruba přečíst jeho kód včetně funkcí.
- Umíš přečíst traceback, rozlišit syntaktickou chybu od chyby za běhu a poznat, kdy výjimka chybu schová.
- Umíš do projektu přidat balíček přes `uv add` a víš, k čemu jsou `pyproject.toml`, `uv.lock` a `.venv`.
- Víš, co je log, znáš úrovně DEBUG, INFO, WARNING, ERROR a CRITICAL a umíš nechat agenta přidat do programu logování.
- Umíš nechat AI shrnout log a její závěr ověřit v datech a kódu.
