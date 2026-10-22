---
id: crm
title: Aplikace CRM
---

# Aplikace CRM

Zatím jsi psal(a) programy, které běží v terminálu: vypíšou výsledek a skončí. Většina aplikací, které denně používáš, ale vypadá jinak. Otevřeš je v prohlížeči, klikáš na tlačítka, vyplňuješ formuláře a data v nich zůstávají. Dnes takovou aplikaci začneš stavět. Postavíš ji v Pythonu pomocí *Djanga*, balíčku pro tvorbu webových aplikací, který si do projektu přidáš přes `uv add` stejně jako `requests`.

## Co budeme stavět: CRM

> **Kdy se to hodí:** Malá firma dělá weby pro jiné firmy. Obchodníci mají kontakty v e-mailech, rozjednané zakázky v tabulce a stav jednání v hlavě. Když někdo onemocní, nikdo neví, komu se má ozvat a jak daleko je jednání.

Postavíme *CRM* (z anglického *Customer Relationship Management*, česky řízení vztahů se zákazníky). Je to aplikace, do které firma zapisuje své zákazníky a obchody, aby všichni věděli, v jakém stavu jsou. Používá ji skoro každá firma, která něco prodává.

Naše CRM bude evidovat dvě věci:

- **Firmy**, tedy zákazníky nebo možné zákazníky: název, IČO, e-mail, telefon a stav. Stav říká, jak daleko je firma od toho, aby u nás nakupovala: nová, lead (projevila zájem), příležitost, aktivní zákazník, bývalý zákazník, neaktivní.
- **Obchodní případy**, tedy konkrétní rozjednané obchody: u které firmy, popis, hodnota v Kč a fáze. Fáze ukazuje, kde je obchod v obchodním procesu: vyhledávání, analýza, nabídka, vyjednávání, a nakonec uzavřeno – získáno, nebo uzavřeno – ztraceno.

Na stránce budou seznamy firem a obchodních případů a formuláře, kterými přidáš nové. Do budoucna můžeme přidat třeba lidi z firem (kontakty) nebo záznamy o schůzkách.

Tenhle seznam funkcí ale agentovi jen tak nepředáš. V další části se k němu s agentem dopracuješ v brainstormingu: agent se tě vyptá, jak firma prodává a co CRM potřebuje, a sepíše návrh.
