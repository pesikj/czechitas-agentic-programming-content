---
id: shrnuti
title: Shrnutí
---

# Shrnutí

- Víš, že automatický test je program, který připraví situaci, provede akci a ověří výsledek. Umíš testy CRM spustit v Dockeru (`docker compose exec web uv run python manage.py test`) a z výpisu poznat, který test selhal a proč.
- Víš, že jednotkový test kontroluje jednu malou část kódu bez databáze a prohlížeče, a umíš s agentem přes TDD přidat funkci, jako je kontrola IČO.
- Víš, že integrační test ověřuje spolupráci víc částí, třeba formuláře, databáze a stránky, a že Django pro testy vytváří samostatnou testovací databázi.
- Umíš nainstalovat Playwright, nahrát test příkazem `codegen` a spustit ho proti běžící aplikaci. Víš, že testy v prohlížeči jsou nejpomalejší a nejkřehčí, a proto jich píšeš nejméně.
- Víš, že zelené testy ještě neznamenají, že aplikace dělá, co má. Test od agenta si ověříš tak, že rozbiješ kód a podíváš se, jestli selže, a v pull requestu hlídáš, jestli agent testy neoslabil.
