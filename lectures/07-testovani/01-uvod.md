---
id: uvod
title: Úvod
---

# Testování aplikace

Minule jsi zjistil(a), jak CRM ukládá data do databáze, a s agentem jsi aplikaci přesunul(a) do Dockeru. Agent už při stavbě CRM psal testy, ty jsi je ale jen spouštěl(a). Dnes zjistíš, co v nich je, a naučíš se je s agentem psát:

1. **Proč testovat** – co je automatický test a proč se bez něj při práci s agentem neobejdeš.
2. **Jednotkové testy** – jak otestovat jednu malou část kódu, třeba kontrolu IČO.
3. **Integrační testy** – jak ověřit, že formulář, databáze a stránka fungují dohromady.
4. **Testy v prohlížeči s Playwright** – jak nechat program proklikat aplikaci stejně, jako by to udělal člověk.
5. **Testy a AI agent** – jak poznat, že test od agenta opravdu něco hlídá.

**Proč to potřebuješ:** Každá změna od agenta může rozbít něco, co předtím fungovalo, a často na úplně jiném místě, než na kterém agent pracoval. Proklikat po každé změně celou aplikaci ručně nejde, testy to zvládnou za pár vteřin. A protože testy často píše i agent, musíš umět poznat, jestli opravdu něco hlídají: zelený výsledek ještě neznamená, že aplikace dělá, co má.

**Po lekci budeš umět:**
- Víš, co je automatický test, a umíš testy CRM spustit v Dockeru a přečíst jejich výsledek.
- Víš, čím se liší jednotkové, integrační a end-to-end testy, a umíš u funkce rozhodnout, který druh testu se na ni hodí.
- Umíš s agentem přidat funkci přes TDD i s jednotkovými a integračními testy.
- Umíš nainstalovat Playwright a spustit test, který aplikaci proklikne v prohlížeči.
- Umíš ověřit, že test od agenta opravdu selže, když se kód rozbije.
