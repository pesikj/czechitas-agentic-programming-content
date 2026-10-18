---
id: kam-dal
title: Kam dál
---

# Kam dál

- **Přidej varování.** Požádej agenta, aby do `nakup.log` zapsal `WARNING`, když položka nemá vyplněnou měnu. Smaž u jedné položky měnu a ověř, že se varování v logu objevilo.
- **Zapni podrobný log.** Změň v `logging.basicConfig` úroveň z `logging.INFO` na `logging.DEBUG` a nech agenta přidat zprávu `DEBUG` u každého převodu eur. Porovnej, o kolik je log delší a co nového z něj vyčteš.
- **Nech AI číst cizí log.** Spusť program několikrát s různými chybami v datech a pak nech agenta log shrnout. Najdi v datech, jestli jeho vysvětlení sedí.

- **Prohlédni si historii cizího projektu.** Otevři na GitHubu [repozitář balíčku requests](https://github.com/psf/requests) a podívej se na seznam commitů a otevřené pull requesty. Vyber jeden commit a zkus z popisu a změněných řádků říct, co se v něm změnilo.

Chceš vědět víc? [Logging HOWTO v dokumentaci Pythonu](https://docs.python.org/3/howto/logging.html) · [Kniha Pro Git v češtině](https://git-scm.com/book/cs/v2)

Příště se podíváš podrobněji na cykly a funkce a na to, jak rozdělit program na menší části, ve kterých se vyznáš ty i agent.
