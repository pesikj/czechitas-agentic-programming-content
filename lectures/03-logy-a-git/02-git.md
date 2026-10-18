---
id: git
title: Git
---

# Git: historie verzí programu

Log ti řekne, co program dělal. Co když ale program přestane fungovat proto, že se změnil kód? Pak potřebuješ vědět, co přesně se změnilo, a umět se vrátit k verzi, která fungovala.

## Co je Git

> **Kdy se to hodí:** Požádáš agenta, aby do `nakup.py` přidal převod dolarů. Agent upraví tři místa v kódu a program najednou počítá špatně i eura. Chceš vidět, co přesně změnil, a vrátit se k verzi, která fungovala.

Představ si, že píšeš diplomovou práci. Jednoho dne smažeš celou kapitolu, protože ji chceš napsat lépe, a pak zjistíš, že původní verze byla lepší. Nebo na stejném dokumentu pracujete dva a navzájem si přepisujete změny.

Přesně tohle řeší [Git](https://git-scm.com). Je to *systém pro správu verzí* (anglicky *version control system*): sleduje každou změnu v souborech projektu, pamatuje si historii všech uložených verzí a umožní ti se k nim kdykoli vrátit. Umí také sloučit práci více lidí dohromady.

Složce projektu, jejíž historii Git sleduje, se říká *repozitář* (anglicky *repository*). Tvůj projekt `nakup` se repozitářem stane, jakmile v něm Git zapneš příkazem `git init`. Git máš nainstalovaný z lekce 01 a funguje čistě na tvém počítači: historii si prohlédneš i bez internetu. Internet potřebuješ až tehdy, když chceš kód sdílet nebo zálohovat.

## Proč Git používat

- **Historie změn.** Každá uložená verze kódu zůstane zachovaná. Když nová úprava něco rozbije, podíváš se, co přesně se změnilo, a vrátíš se k verzi, která fungovala.
- **Záloha.** Kód uložený jen ve tvém počítači zmizí s jeho poruchou. S Gitem můžeš mít kopii i na serveru na internetu.
- **Spolupráce.** Na jednom projektu může pracovat víc lidí najednou. Git sleduje, kdo co změnil, a pomůže změny spojit.
- **Přenositelnost.** Projekt v Gitu si stáhneš na jakýkoli počítač nebo ho předáš jinému nástroji, třeba z Codexu v terminálu do Claude Code nebo do desktopové aplikace, a pokračuješ tam, kde jsi skončil(a).
- **Větve.** Chceš vyzkoušet novou funkci, aniž bys rozbil(a) program, který funguje? Zkoušíš ji v oddělené větvi a do hlavní verze ji přidáš, až když funguje (víc níže).

## GitHub, GitLab a další servery

Aby ses mohl(a) o kód dělit nebo ho zálohovat, potřebuješ místo na internetu, kde bude uložený. Takové kopii repozitáře na serveru se říká *vzdálený repozitář* (anglicky *remote repository*). Nejznámější služby, které je nabízejí:

- **[GitHub](https://github.com)** – největší platforma s miliony veřejných projektů, patří Microsoftu. Veřejné i soukromé repozitáře má zdarma. Účet sis na něm založil(a) v lekci 01.
- **[GitLab](https://gitlab.com)** – oblíbený ve firmách, protože si ho mohou provozovat na vlastním serveru a data neopustí firmu.
- **[Bitbucket](https://bitbucket.org)** – od firmy Atlassian, používají ho hlavně týmy, které pracují s jejími nástroji Jira a Confluence.

Všechny tři pracují s Gitem stejně, liší se doplňkovými funkcemi a cenou. GitHub je zároveň místem, kde žije spousta veřejně dostupného softwaru. Najdeš tam třeba i [balíček requests](https://github.com/psf/requests), který jsi minule přidal(a) do projektu.

## Základní operace

**Commit – uložení verze.** *Commit* je pojmenovaný snímek aktuálního stavu projektu. Je to jako uložení hry: v tuhle chvíli víš, že program funguje, a chceš mít možnost se sem vrátit.

```bash
git add .
git commit -m "Převod eur aktuálním kurzem ČNB"
```

`git add .` vybere všechny změněné soubory, které se mají uložit. `git commit -m` vytvoří snímek s popisem v uvozovkách. Popis piš tak, abys i za měsíc věděl(a), co se v té verzi změnilo.

**Co se změnilo: status, diff a log.** Než commit uděláš, můžeš se podívat, co v projektu přibylo. `git status` vypíše, které soubory se od posledního commitu změnily. `git diff` ukáže přímo změněné řádky: co přibylo a co zmizelo. `git log` vypíše historii commitů s jejich popisy.

**Push – odeslání na server.** *Push* odešle tvoje commity z počítače do vzdáleného repozitáře, třeba na GitHub. Ostatní lidé nebo jiné nástroje si je pak mohou stáhnout.

```bash
git push
```

**Pull – stažení změn ze serveru.** *Pull* stáhne do počítače commity, které na server poslal někdo jiný, nebo ty sám(a) z jiného počítače.

```bash
git pull
```

**Clone – stažení celého repozitáře.** *Clone* použiješ, když chceš na svém počítači pracovat s projektem, který zatím máš jen na serveru. Stáhne celý kód včetně kompletní historie:

```bash
git clone https://github.com/psf/requests.git
```

Git vytvoří složku `requests` s celým projektem. Adresu repozitáře najdeš na GitHubu pod tlačítkem **Code**.

## Větev, pull request a merge

> **Kdy se to hodí:** Chceš do programu přidat převod dolarů, ale nechceš riskovat, že rozbiješ verzi, která správně počítá koruny a eura.

*Větev* (anglicky *branch*) je samostatná linie historie projektu, ve které můžeš zkoušet změny bez dopadu na hlavní verzi. Hlavní větev se obvykle jmenuje `main`.

```bash
git switch -c prevod-dolaru
```

Příkaz vytvoří novou větev `prevod-dolaru` a přepne tě do ní. Commity, které teď uděláš, se uloží jen do ní. Větev `main` zůstane, jak byla.

Když je změna hotová a vyzkoušená, odešleš větev na GitHub (`git push`) a vytvoříš *pull request* (zkráceně *PR*): návrh, aby se změny z tvé větve přidaly do `main`. GitHub v něm ukáže, které soubory se změnily a které řádky přibyly nebo zmizely, a ostatní k nim mohou psát komentáře. Když je s PR všechno v pořádku, klikneš na **Merge pull request**. Tím se změny sloučí do `main` (anglicky *merge*) a větev `prevod-dolaru` můžeš smazat.

## Git a AI agent

Git je pojítko mezi nástroji i mezi tebou a agentem. Pátý krok postupu agentního programování z minulé lekce, **Ulož**, v praxi znamená právě commit. Z toho plyne jednoduché pravidlo: **než necháš agenta měnit kód, udělej commit verze, která funguje.** Když se úprava nepovede, máš se kam vrátit.

Po práci agenta se podívej na `git diff`. Uvidíš přesně ty řádky, které agent změnil, a ne jen jeho popis toho, co udělal. Tak poznáš, jestli změnil jen to, o co jsi žádal(a).

Codex i Claude Code umějí pracovat i přímo s repozitářem na GitHubu, bez tvého počítače: na webu jim zadáš úkol a výsledek ti předloží jako pull request ke schválení. I tady platí, co už znáš: změny si před sloučením přečti.
