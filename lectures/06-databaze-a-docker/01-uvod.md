---
id: uvod
title: Úvod
---

# Databáze a Docker

Minule jsi s agentem postavil(a) první verzi CRM v Djangu: firmy a obchodní případy, které přidáš přes formulář a které po restartu serveru nezmizí. Dnes se podíváš, kam se vlastně ukládají, a připravíš aplikaci na život mimo tvůj počítač:

1. **Databáze v Djangu** – jak Django ukládá data do databáze SQLite, co jsou tabulky, modely a migrace a jak se na data podíváš.
2. **Docker** – co je kontejner a proč se aplikace balí do Dockeru.
3. **Docker Compose** – jak s agentem převedeš CRM na dva kontejnery: aplikaci a samostatnou databázi.

**Proč to potřebuješ:** Agent za tebe napsal modely i migrace, ale když se něco s daty pokazí, musíš vědět, kde hledat. Bez představy o tom, jak databáze funguje, nepoznáš, jestli agent data jen přejmenoval, nebo je smazal. Docker pak řeší problém "u mě to funguje": aplikace poběží všude stejně, na tvém počítači, u kolegyně i na serveru, kam ji později v kurzu nasadíš.

**Po lekci budeš umět:**
- Víš, co je databáze, tabulka a řádek a jak z modelů v Djangu vznikají tabulky přes migrace.
- Umíš se na data podívat přes administraci i přes Django shell a umíš nechat agenta bezpečně přidat do modelu nové pole.
- Víš, co je Docker, obraz, kontejner a Docker Compose a k čemu slouží.
- Umíš s agentem převést aplikaci na Docker Compose s kontejnerem pro aplikaci a pro databázi a ověřit, že funguje.
