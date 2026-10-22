---
id: kam-dal
title: Kam dál
---

# Kam dál

- **Otestuj obchodní případy.** Nech agenta přidat integrační test, který ověří, že obchodní případ nejde uložit se zápornou hodnotou. Pokud to aplikace zatím dovolí, máš první chybu nalezenou testem.
- **Sleduj Playwright při práci.** Spusť test v prohlížeči s přepínači `--headed --slowmo 500`. Uvidíš, jak Playwright vyplňuje formulář pomalu krok po kroku.
- **Nech testy spouštět GitHub.** Zeptej se agenta, jak nastavit GitHub Actions, aby se testy spustily při každém pull requestu. Vytvoř pull request a podívej se, jestli se u něj výsledek testů objevil.
- **Najdi slabý test.** Projdi testy v `obchod/tests.py` a najdi aspoň jeden, který by prošel, i kdyby kód nefungoval. Zeptej se agenta, jak ho zpřísnit.

Chceš vědět víc? [Testování v Djangu](https://docs.djangoproject.com/en/stable/topics/testing/overview/) · [Playwright pro Python](https://playwright.dev/python/docs/intro)

Příště CRM nasadíš na internet, na službu Railway, aby ho obchodníci Webovky mohli používat ze svých počítačů.
