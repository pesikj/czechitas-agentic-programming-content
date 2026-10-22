---
id: nastaveni-agenta
title: Nastavení agenta
---

# Nastavení agenta

Víš, co je AI agent a že práci řídíš ty. Než mu v příští lekci necháš psát program, podíváš se, jak ho nastavit. Agent má čtyři nastavení, která ovlivní každou jeho práci:

- **Režim oprávnění** – co smí udělat sám a na co se tě musí zeptat.
- **Model** – jak "chytrý" mozek za agentem pracuje.
- **Úroveň přemýšlení** – jak dlouho model přemýšlí, než odpoví.
- **Limity používání** – kolik práce ti předplatné dovolí a kolik ti ještě zbývá.

Všechna čtyři si vyzkoušíš v projektu `nakup` z minulé části. Otevři ho ve VS Code a spusť agenta v terminálu ve VS Code (příkazem `codex` nebo `claude`), nebo v desktopové aplikaci vyber jako projekt složku `nakup`.

## Režim oprávnění: co smí agent sám

> **Kdy se to hodí:** Požádáš agenta o program na sčítání nákupu. Agent chce vytvořit soubor `nakup.py`, pak ho spustit a nakonec si do projektu stáhnout balíček z internetu. U každého kroku se tě ptá, jestli smí. Po desáté otázce tě to začne zdržovat, ale nechceš, aby bez ptaní mazal soubory mimo projekt.

Agent umí číst soubory, upravovat je a spouštět příkazy v terminálu. *Režim oprávnění* (anglicky *permission mode*) určuje, co z toho smí udělat sám a před čím se tě zeptá. Je to jako s novou kolegyní: první dny jí každý krok kontroluješ, a jak roste důvěra, necháš ji běžné věci dělat samostatně. Důležité zásahy ale chceš vidět vždycky.

Režimy se v Codexu a Claude Code jmenují jinak, ale fungují podobně:

::::alternatives
:::option{label="Codex"}
| Režim | Co agent dělá sám | Na co se ptá |
|---|---|---|
| **Ask for approval** | čte a upravuje soubory a spouští příkazy uvnitř projektu | na práci mimo složku projektu a na přístup k internetu |
| **Approve for me** | totéž, a navíc sám schvaluje bezpečně vypadající požadavky | jen na akce, které vypadají riskantně |
| **Full access** | úplně všechno, na celém počítači i na internetu | na nic |

V desktopové aplikaci přepneš režim ovládacím prvkem pod polem pro zprávu. V terminálu napiš příkaz `/permissions` a režim vyber ze seznamu.

Codex pracuje v *sandboxu* (česky "pískoviště"): v uzavřeném prostoru, ze kterého bez tvého svolení nedosáhne mimo složku projektu. Proto je i režim Ask for approval docela samostatný a ptá se jen na důležité věci. V terminálu se nabídka režimů může jmenovat trochu jinak (třeba Read Only, Auto), význam je stejný: od "jen čti" po "dělej, co chceš".
:::
:::option{label="Claude Code"}
| Režim | Co agent dělá sám | Na co se ptá |
|---|---|---|
| **Manual** | jen čte soubory | na každou úpravu souboru a každý příkaz |
| **Edit automatically** | čte a upravuje soubory v projektu a spouští jednoduché příkazy (vytvoření složky, přesun souboru) | na ostatní příkazy |
| **Plan** | jen čte a navrhuje plán | nic nemění |
| **Auto** | skoro všechno; každou akci předem zkontroluje druhý model a riskantní zastaví | jen na to, co kontrola zastaví |
| **Bypass permissions** | úplně všechno, bez kontroly | na nic |

V terminálu přepínáš režimy klávesami `Shift Tab`. Aktuální režim vidíš pod polem pro zprávu, třeba `⏸ manual mode on` nebo `⏵⏵ accept edits on`. V desktopové aplikaci a ve VS Code vybereš režim přepínačem u pole pro zprávu.

Nové verze Claude Code začínají v režimu Auto. Na začátku kurzu je lepší přepnout na Manual nebo Edit automatically, abys viděl(a), co agent dělá.
:::
::::

**Jaký režim zvolit?** Dokud se učíš, používej režim, ve kterém se tě agent ptá před spuštěním příkazů: v Codexu **Ask for approval**, v Claude Code **Manual** nebo **Edit automatically**. Uvidíš tak, co agent dělá, a naučíš se jeho příkazy číst. Režimy **Full access** a **Bypass permissions** nepoužívej. Jsou určené pro uzavřená prostředí, kde agent nemůže nic pokazit.

Když se tě agent zeptá, máš obvykle tři možnosti: povolit jednou, povolit podobné akce na celou konverzaci, nebo odmítnout. Než odpovíš, přečti si, co přesně chce udělat, stejně jako u výpisu složky Dokumenty v části o terminálu. Když nevíš, co příkaz dělá, odmítni ho a zeptej se agenta:

```text
Proč chceš spustit tenhle příkaz? Co přesně udělá?
```

## Model: jaký mozek pracuje

> **Kdy se to hodí:** Chceš v `nakup.py` přejmenovat proměnnou `kurz` na `kurz_eur`. Na to nepotřebuješ nejsilnější model, který přemýšlí minutu a spotřebuje hodně z tvého limitu. Na návrh celé aplikace se ti naopak silný model vyplatí.

Z minulé části víš, že agent je nástroj a za ním pracuje jazykový model. Ten si můžeš vybrat. Velké modely zvládnou složitější úkoly a dělají méně chyb, ale jsou pomalejší a víc čerpají z tvého limitu. Malé modely jsou rychlé a úsporné a na jednoduché úkoly stačí. Je to jako ve firmě: na návrh nového systému pozveš zkušenou architektku, na přejmenování souboru ji volat nemusíš.

Nabídka modelů se mění s každou novou verzí, proto si vždy zkontroluj, co je k dispozici zrovna u tebe:

::::alternatives
:::option{label="Codex"}
V desktopové aplikaci vybereš model ovládacím prvkem pod polem pro zprávu. V terminálu napiš `/model` a vyber ze seznamu.

V době psaní lekce OpenAI doporučuje model **GPT-6.1 Sol** pro běžné programování a menší **GPT-6 Luna** pro jednoduché, opakované úkoly.
:::
:::option{label="Claude Code"}
V terminálu napiš `/model` a vyber ze seznamu. Můžeš napsat i rovnou `/model sonnet`. V desktopové aplikaci vybereš model u pole pro zprávu.

Modely Claude mají tři hlavní řady:

- **Opus** – nejsilnější, na složité úkoly a plánování.
- **Sonnet** – na běžné programování.
- **Haiku** – nejrychlejší, na jednoduché úkoly.
:::
::::

V tomhle kurzu ti bude stačit model, který nástroj nabízí jako výchozí. Na menší model přepni, když se blížíš k limitu nebo děláš jednoduchou úpravu. Na silnější, když si agent s úkolem opakovaně neví rady.

## Úroveň přemýšlení: jak dlouho model přemýšlí

> **Kdy se to hodí:** Agent ti rychle odpoví, ale v programu přehlédne, že část cen je v eurech. Když ho necháš přemýšlet déle, víc si zkontroluje a chybu najde sám. Na jednoduchou otázku ale dlouhé přemýšlení nepotřebuješ.

Moderní modely si před odpovědí nejdřív samy pro sebe rozmyslí postup, podobně jako ty v pseudokódu. *Úroveň přemýšlení* (anglicky *reasoning effort*, v Claude Code jen *effort*) určuje, kolik času tomu věnují. Vyšší úroveň znamená pečlivější práci u složitých úkolů, ale delší čekání a vyšší spotřebu limitu. Nižší úroveň je rychlá a úsporná.

::::alternatives
:::option{label="Codex"}
Úrovně jsou **Light**, **Medium**, **High** a **Extra High**, podle nastavení i vyšší. V terminálu se nejnižší úroveň jmenuje **Low**.

V desktopové aplikaci úroveň vybereš ve stejném ovládacím prvku jako model, pod polem pro zprávu. V terminálu ji nastavíš příkazem `/model`: po výběru modelu se tě zeptá i na úroveň přemýšlení.
:::
:::option{label="Claude Code"}
Úrovně jsou **low**, **medium**, **high**, **xhigh** a **max**. U nejnovějších modelů je výchozí úroveň medium.

V terminálu napiš `/effort` a úroveň vyber posuvníkem, nebo ji zadej rovnou, třeba `/effort high`. Úroveň můžeš změnit i v nabídce `/model` šipkami doleva a doprava.

Když chceš, aby model důkladně přemýšlel jen u jedné zprávy, napiš do ní slovo `ultrathink`. Nastavení pro další zprávy se tím nezmění.
:::
::::

Pro běžnou práci v kurzu stačí střední úroveň. Vyšší zapni na plánování větší aplikace nebo na chybu, kterou agent nedokáže opravit. Nižší na drobné úpravy, kde chceš rychlou odpověď.

## Limity používání: kolik ti zbývá

> **Kdy se to hodí:** Jsi uprostřed cvičení a agent najednou přestane pracovat s hláškou, že jsi dosáhl(a) limitu. Kdybys věděl(a), že se k limitu blížíš, mohl(a) jsi přepnout na menší model a cvičení dokončit.

Předplatné ChatGPT i Claude ti nedává neomezenou práci s agentem. Obsahuje určitý objem práce, který se měří v časových oknech: obvykle **pětihodinové okno** (krátkodobý limit, který se po pár hodinách obnoví) a **týdenní okno**. Abys mohl(a) pracovat, musí ti zbývat v obou. Kolik přesně dostaneš, závisí na tvém předplatném.

Limit se nepočítá podle počtu zpráv, ale podle toho, kolik práce model udělá. Nejvíc ho čerpá:

- **silnější model** a **vyšší úroveň přemýšlení**,
- **dlouhá konverzace** – agent s každou zprávou znovu zpracuje celou dosavadní konverzaci, takže i krátká otázka na konci dlouhého rozhovoru stojí hodně,
- **velký úkol** – agent čte mnoho souborů a spouští mnoho příkazů.

Kolik ti zbývá, zjistíš takhle:

::::alternatives
:::option{label="Codex"}
V terminálu napiš `/status`. Uvidíš aktuální model, režim oprávnění a zbývající limity. Podrobnější přehled spotřeby ukáže `/usage`.

Kdykoli můžeš limity a čas jejich obnovení zkontrolovat i na webu v [nastavení Codexu](https://chatgpt.com/codex/settings/usage).
:::
:::option{label="Claude Code"}
V terminálu napiš `/usage`. Uvidíš ukazatele zaplnění pětihodinového i týdenního limitu, čas jejich obnovení a doporučení, jak spotřebu snížit.

Stejné údaje najdeš i na webu v [nastavení Claude](https://claude.ai/settings/usage) v části **Usage**, nebo v desktopové aplikaci v **Settings → Usage**.
:::
::::

Když se blížíš k limitu:

- **Přepni na menší model nebo nižší úroveň přemýšlení.** Na dokončení cvičení většinou stačí.
- **Začni novou konverzaci**, když přecházíš k jinému úkolu. V Codexu příkazem `/new`, v Claude Code příkazem `/clear`. Agent pak nemusí s každou zprávou zpracovávat starý rozhovor.
- **Počkej na obnovení.** Čas obnovení vidíš ve výpisu limitů.

Obě služby nabízejí možnost dokoupit si práci navíc. Na tenhle kurz by ti měl stačit limit, který máš v předplatném.

## Cvičení: Prozkoumej nastavení svého agenta

Zjisti, jak je tvůj agent nastavený, a vyzkoušej si, jak se nastavení projeví v jeho práci.

1. Zjisti, v jakém režimu oprávnění, s jakým modelem a s jakou úrovní přemýšlení agent běží. Přepni ho do režimu, ve kterém se ptá před spuštěním příkazů (v Codexu **Ask for approval**, v Claude Code **Manual**).
2. Zkontroluj, kolik ti zbývá z limitů, a zapiš si to.
3. Zadej agentovi úkol. Prompt pro agenta:

   ```text
   Vytvoř ve složce soubor ahoj.py, který vypíše "Ahoj, Czechitas!",
   a spusť ho příkazem uv run ahoj.py.
   ```

   Na co se tě agent ptal? Než akci povolíš, přečti si, co chce udělat.
4. Znovu zkontroluj limity. Změnilo se něco?
5. Přepni na nejmenší model a nejnižší úroveň přemýšlení a zadej stejný úkol znovu (soubor předtím smaž). Lišila se rychlost nebo výsledek? Nakonec vrať výchozí nastavení.

```exercise
id: nastaveni-agenta
revision: 1
title: Prozkoumej nastavení svého agenta
fields:
  - id: nastaveni
    label: Výchozí nastavení agenta
    guidance: V jakém režimu oprávnění, s jakým modelem a s jakou úrovní přemýšlení agent běžel?
  - id: schvalovani
    label: Na co se tě agent ptal
    guidance: Které akce chtěl agent udělat? Povolil(a) jsi všechny? Rozuměl(a) jsi každému příkazu?
  - id: limity
    label: Limity před úkolem a po něm
    guidance: Kolik ti zbývalo z pětihodinového a týdenního limitu? Změnilo se to po úkolu viditelně?
  - id: porovnani
    label: Menší model a nižší úroveň přemýšlení
    guidance: Byl agent rychlejší? Lišil se výsledek? Kdy bys takové nastavení použil(a)?
```
