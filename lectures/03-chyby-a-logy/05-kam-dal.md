---
id: kam-dal
title: Kam dál
---

# Kam dál

- **Rozbij program jinak.** Smaž v `nakup.csv` celý sloupec `mena` nebo přejmenuj soubor a podívej se, jakou výjimku program vyhodí. Zkus traceback přečíst sám(a), než ho ukážeš agentovi.
- **Přidej varování.** Požádej agenta, aby do `nakup.log` zapsal `WARNING`, když položka nemá vyplněnou měnu. Smaž u jedné položky měnu a ověř, že se varování v logu objevilo.
- **Zapni podrobný log.** Změň v `logging.basicConfig` úroveň z `logging.INFO` na `logging.DEBUG` a nech agenta přidat zprávu `DEBUG` u každého převodu eur. Porovnej, o kolik je log delší a co nového z něj vyčteš.
- **Nech AI číst cizí log.** Spusť program několikrát s různými chybami v datech a pak nech agenta log shrnout. Najdi v datech, jestli jeho vysvětlení sedí.

Chceš vědět víc? [Logging HOWTO v dokumentaci Pythonu](https://docs.python.org/3/howto/logging.html) · [Dokumentace uv](https://docs.astral.sh/uv/)

Příště začneš ukládat verze programu v Gitu, aby ses mohl(a) k funkční verzi kdykoli vrátit, a novou funkci přidáš přes větev a pull request.
