---
id: macos
title: Instalace na macOS
---

# Instalace na macOS

Před začátkem kurzu si připravte **Homebrew**, **uv**, **Python**, **Git**, **Visual Studio Code** a účet na **GitHubu**. **Docker Desktop** budeme potřebovat až později v kurzu. Pokud už některý nástroj máte, stačí ověřit jeho funkčnost podle posledního kroku.

## 1. Homebrew

Otevřete aplikaci **Terminál** (najdete ji přes Spotlight pomocí `⌘ mezerník`). Spusťte instalační příkaz z [oficiálního webu Homebrew](https://brew.sh/):

```bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

Instalátor může požádat o heslo k Macu; při jeho psaní se znaky nezobrazují. Pokud nabídne instalaci **Command Line Tools**, nechte ji dokončit.

Na konci spusťte příkazy, které instalátor vypíše v části **Next steps** pro přidání Homebrew do `PATH`. Potom zavřete a znovu otevřete Terminál.

## 2. uv a Git

Nainstalujte [uv](https://docs.astral.sh/uv/getting-started/installation/#homebrew) a [Git](https://git-scm.com/install/mac) pomocí Homebrew:

```bash
brew install uv git
```

## 3. Python pomocí uv

Nainstalujte [Python pomocí uv](https://docs.astral.sh/uv/guides/install-python/):

```bash
uv python install
```

## 4. Visual Studio Code

Nainstalujte [Visual Studio Code](https://formulae.brew.sh/cask/visual-studio-code):

```bash
brew install --cask visual-studio-code
```

## 5. Docker Desktop – na pozdější část kurzu

Stáhněte [Docker Desktop pro macOS](https://docs.docker.com/desktop/setup/install/mac-install/): variantu **Apple silicon** pro čipy řady M, nebo **Intel** pro starší Macy. Typ čipu najdete v nabídce ** → O tomto Macu**.

Otevřete soubor `.dmg`, přesuňte Docker do **Aplikací** a spusťte jej. Dokončete úvodní nastavení a počkejte na spuštění enginu. Instalaci můžete odložit, dokud Docker nebudeme v kurzu používat.

## 6. Registrace na GitHubu

Vytvořte si [bezplatný účet na GitHubu](https://github.com/signup) a ověřte e-mailovou adresu. Pokud účet už máte, ověřte, že se do něj můžete přihlásit.

## 7. Codex nebo Claude Code – aplikace a CLI

Vyberte produkt, který máte předplacený s přístupem ke kódovacímu agentovi. Nainstalujte jeho **desktopovou aplikaci i CLI** (verzi pro příkazový řádek). Stačí jedna z následujících variant.

::::alternatives
:::option{label="Codex"}
Nainstalujte [desktopovou aplikaci ChatGPT](https://formulae.brew.sh/cask/chatgpt) a [Codex CLI](https://formulae.brew.sh/cask/codex):

```bash
brew install --cask chatgpt codex
```

Otevřete **ChatGPT** z Aplikací, přihlaste se účtem s předplatným a vyberte [režim **Codex**](https://learn.chatgpt.com/docs/app).

V novém okně Terminálu ověřte instalaci příkazem `codex --version`. Potom spusťte `codex` a zvolte přihlášení přes **ChatGPT** se stejným účtem jako v aplikaci.
:::
:::option{label="Claude Code"}
Nainstalujte [desktopovou aplikaci Claude](https://formulae.brew.sh/cask/claude) a [Claude Code CLI](https://code.claude.com/docs/en/setup):

```bash
brew install --cask claude claude-code
```

Otevřete **Claude** z Aplikací, přihlaste se účtem s předplatným a otevřete záložku **Code**.

V novém okně Terminálu ověřte instalaci příkazem `claude --version`. Potom spusťte `claude` a přihlaste se účtem s předplatným **Claude**, který používáte v aplikaci.
:::
::::

## 8. Ověření instalace

V novém okně Terminálu postupně spusťte:

```bash
brew --version
uv --version
uv run python --version
git --version
code --version
```

Každý příkaz má vypsat verzi nástroje. Potom spusťte `code` a ověřte, že se otevře Visual Studio Code.

Pokud jste nainstalovali Docker, nechte Docker Desktop spuštěný a zadejte `docker version`. Výstup má obsahovat části **Client** i **Server**.

Pokud Terminál nezná příkaz `brew`, zkontrolujte krok **Next steps**. S ostatními chybami pošlete lektorovi příkaz a chybovou zprávu.
