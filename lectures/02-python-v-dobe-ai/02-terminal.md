---
id: terminal
title: Terminál
---

# Terminál: jak s počítačem mluví AI

Začínáme terminálem, protože ho budeš potřebovat ve všech dalších částech: v terminálu spouštíš programy, ověřuješ nainstalované nástroje a v terminálu pracuje i AI agent.

## Jak zjistit, co je ve složce Dokumenty?

> **Kdy se to hodí:** Chceš vědět, jaké soubory máš ve složce Dokumenty. Pro tebe je to pár kliknutí. Co ale musí udělat AI, aby ti odpověděla?

### Cesta pro člověka: okna a myš

Ty otevřeš **Průzkumník souborů** (Windows) nebo **Finder** (macOS), klikneš na složku Dokumenty a vidíš její obsah: ikony, názvy souborů, data změn. Je to pohodlné, protože celé rozhraní je postavené pro lidské oči a ruku s myší.

Takovému rozhraní se říká *grafické rozhraní* (anglicky *graphical user interface*, zkráceně *GUI*). Informace v něm jsou obrázky na obrazovce.

### Jak by to zvládla AI?

Jazykový model pracuje s textem. Kdyby měl použít stejnou cestu jako ty, musel by:

1. převzít kontrolu nad obrazovkou, myší a klávesnicí,
2. najít a otevřít Průzkumník nebo Finder,
3. kliknout na složku Dokumenty,
4. udělat snímek obrazovky,
5. ze snímku "přečíst" názvy souborů a převést je na text.

Jde to – některé nástroje to opravdu umějí. Je to ale pomalé a křehké. Stačí jiné rozložení oken, vyskakovací okno nebo dlouhý název souboru, který se nevejde celý, a AI se splete.

### Druhá cesta: terminál

Počítač naštěstí umí komunikovat i jinak. *Terminál* (anglicky *terminal*) je textové rozhraní: počítači napíšeš *příkaz* (anglicky *command*) a on ti odpoví textem. Žádné ikony, žádná myš – jen text tam a text zpátky.

Obsah složky Dokumenty zjistíš dvěma příkazy:

- `cd Documents` – *change directory*, přejdi do složky Documents,
- `ls` – *list*, vypiš, co ve složce je.

Složka, kterou Průzkumník i Finder v češtině ukazují jako **Dokumenty**, se ve skutečnosti jmenuje `Documents`. V terminálu proto vždy používej anglický název.

## Vyzkoušej si to

Otevři terminál. Po spuštění se nacházíš ve své *domovské složce* (anglicky *home directory*) – to je složka s tvým uživatelským jménem, ve které jsou Dokumenty, Stažené soubory, Plocha a další.

::::alternatives
:::option{label="Windows"}
Otevři **PowerShell** z nabídky Start, stejně jako při instalaci v lekci 01.

Nejdřív zjisti, kde jsi. Příkaz `pwd` (*print working directory*) vypíše aktuální složku:

```powershell
pwd
```

Výstup (místo `jana` uvidíš svoje uživatelské jméno):

```text
Path
----
C:\Users\jana
```

Přejdi do Dokumentů a vypiš jejich obsah:

```powershell
cd Documents
ls
```

Výstup (tvoje soubory budou jiné):

```text
    Directory: C:\Users\jana\Documents

Mode                 LastWriteTime         Length Name
----                 -------------         ------ ----
d----          12.10.2026    18:03                Faktury
-a---          03.09.2026     9:12          48213 rozpocet.xlsx
-a---          21.08.2026    14:40         102400 zivotopis.pdf
```

Pokud PowerShell hlásí, že složku `Documents` nemůže najít, máš Dokumenty nejspíš uložené ve OneDrivu. Zkus `cd OneDrive\Documents`.
:::
:::option{label="macOS"}
Otevři aplikaci **Terminál**: stiskni `Cmd + mezerník`, napiš `Terminál` a potvrď klávesou Enter.

Nejdřív zjisti, kde jsi. Příkaz `pwd` (*print working directory*) vypíše aktuální složku:

```bash
pwd
```

Výstup (místo `jana` uvidíš svoje uživatelské jméno):

```text
/Users/jana
```

Přejdi do Dokumentů a vypiš jejich obsah:

```bash
cd Documents
ls
```

Výstup (tvoje soubory budou jiné):

```text
Faktury		rozpocet.xlsx	zivotopis.pdf
```

Pokud se macOS zeptá, jestli může Terminál přistupovat ke složce Dokumenty, povol to.
:::
::::

Porovnej výsledek s tím, co vidíš v Průzkumníku nebo ve Finderu. Měly by tam být stejné soubory – jen jednou jako ikony, podruhé jako text.

### Různá terminálová prostředí

Terminál je okno, do kterého píšeš. Příkazy v něm zpracovává program, kterému se říká *shell*. Shellů existuje několik a každý má trochu jiné příkazy:

- **Command Prompt** (`cmd`) – starší shell ve Windows. Obsah složky v něm vypíšeš příkazem `dir`, `ls` nezná.
- **PowerShell** – modernější shell ve Windows. Rozumí `ls` i `dir`. V kurzu ho používáme na Windows.
- **bash** – nejrozšířenější shell v Linuxu. Ve Windows ho dostaneš s Gitem jako *Git Bash*.
- **zsh** – výchozí shell v macOS. Pro běžné příkazy se chová skoro stejně jako bash.

Základní příkazy jako `cd`, `ls` a `pwd` fungují v PowerShellu, bash i zsh. Když se ale návod nebo agent odkazuje na konkrétní příkaz, vyplatí se vědět, v jakém shellu pracuješ.

## Proč terminál vyhovuje AI

Pro člověka působí terminál staromódně. Nic se nedá rozkliknout, příkazy si musíš pamatovat a výpis souborů vypadá strohý. Na druhou stranu vidíš přesně to, co počítač udělal – černé na bílém.

Pro jazykový model je to ideální prostředí. Model umí číst a psát text, a terminál je přesně text dovnitř a text ven. Agent nemusí ovládat myš ani "číst" obrazovku. Spustí příkaz na pozadí, přečte textovou odpověď a pokračuje dalším krokem. Je to rychlé, přesné a dá se to opakovat.

Proto AI agenti jako Codex nebo Claude Code pracují hlavně v terminálu: soubory hledají příkazy, programy spouštějí příkazy a chyby čtou z textového výstupu. A protože všechno probíhá v textu, můžeš si po agentovi každý krok přečíst a zkontrolovat.

## Ukázka: zeptej se agenta

Teď stejný úkol zadáš agentovi. Použij **Codex**, nebo **Claude Code**, podle toho, který máš nainstalovaný – v desktopové aplikaci, nebo v terminálu.

Obyčejný chat v prohlížeči (třeba ChatGPT na webu) tohle nezvládne. Nemá přístup k tvému počítači, takže by ti nanejvýš poradil, jaký příkaz máš spustit sám(a).

::::alternatives
:::option{label="Codex"}
Otevři aplikaci **Codex**, nebo v terminálu spusť příkaz `codex`.
:::
:::option{label="Claude Code"}
Otevři aplikaci **Claude** a záložku **Code**, nebo v terminálu spusť příkaz `claude`.
:::
::::

Prompt pro agenta:

```text
Vypiš názvy souborů a složek v mé složce Dokumenty.
Napiš mi také, jaký příkaz jsi k tomu použil.
```

Agent se tě může před spuštěním příkazu zeptat na povolení. Nejdřív si příkaz přečti – teď už víš, co dělají `cd` a `ls`. Příkaz, který jen vypisuje obsah složky, nic nemaže ani nemění, takže ho můžeš klidně povolit.

V odpovědi agenta, nebo v záznamu jeho práce, najdi příkaz, který spustil. Na macOS to bude nejspíš něco jako `ls ~/Documents`, na Windows `Get-ChildItem` nebo `ls`. Znak `~` je zkratka pro domovskou složku, takže `~/Documents` znamená "Documents v mé domovské složce". Agent tedy udělal přesně to, co ty před chvílí – jen místo dvou příkazů použil jeden.

Pozor na jednu věc: co agent v terminálu přečte, posílá jazykovému modelu na zpracování. Nedávej mu proto procházet složky s citlivými daty, jako jsou hesla nebo zdravotní záznamy.

## Cvičení: Nejnovější a nejstarší soubor

Tentokrát si role prohodíte: AI příkaz jen navrhne a spustíš ho ty. Zjistíš, jaké to je pracovat v terminálu sám(a), a uvidíš, co by jinak agent dělal na pozadí.

Požádej agenta (nebo klidně ChatGPT v prohlížeči – nic spouštět nebude), aby ti napsal příkaz, kterým zjistíš nejnovější a nejstarší soubor nebo složku ve své domovské složce. Do zadání uveď, jaký máš systém a shell, a výslovně napiš, že příkaz nemá spouštět.

Prompt pro agenta:

```text
Pracuji na Windows v PowerShellu (nebo: na macOS v zsh).
Napiš mi příkaz, kterým zjistím nejnovější a nejstarší soubor
nebo složku ve své domovské složce. Příkaz nespouštěj,
jen ho napiš a vysvětli, co dělá která jeho část.
```

Než příkaz spustíš, přečti si ho a vysvětlení. Příkaz má jen vypisovat a řadit – pokud v něm uvidíš něco jako mazání (`rm`, `del`, `Remove-Item`), nespouštěj ho a zeptej se, proč tam je. Pak příkaz zkopíruj do terminálu, spusť ho a z výstupu sám(a) urči nejnovější a nejstarší položku. Pokud příkaz skončí chybou, pošli chybovou hlášku agentovi a požádej o opravu.

Nakonec výsledek ověř seřazením podle data v Průzkumníku nebo ve Finderu.

Všimni si, že zadání není úplně přesné. Znamená "nejstarší" datum vytvoření, nebo poslední změny? A počítají se i skryté soubory? Podívej se, jak si to agent vyložil – a jestli se tě na to zeptal.

```exercise
id: nejnovejsi-nejstarsi
revision: 2
title: Nejnovější a nejstarší soubor
fields:
  - id: prompt
    label: Použitý prompt
  - id: prikaz
    label: Příkaz, který agent navrhl
    guidance: Opiš ho. Co dělá která jeho část? Bylo v něm něco, čemu jsi nerozuměl(a)?
  - id: vystup
    label: Výstup v terminálu
    guidance: Zkopíruj důležitou část výstupu. Fungoval příkaz napoprvé, nebo jsi musel(a) žádat o opravu?
  - id: overeni
    label: Výsledek a ověření
    guidance: Kterou položku jsi z výstupu určil(a) jako nejnovější a kterou jako nejstarší? Shoduje se to s Průzkumníkem nebo Finderem?
  - id: presnost
    label: Jak si agent vyložil "nejstarší"?
    guidance: Podle data vytvoření, nebo změny? Zeptal se tě, nebo si to rozhodl sám?
```
