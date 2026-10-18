---
id: windows
title: Instalace na Windows
---

# Instalace na Windows

Před začátkem kurzu si připravte **Visual Studio Code**, **Git**, **uv**, **Python** a účet na **GitHubu**. **Docker Desktop** budeme potřebovat až později v kurzu. Pokud už některý nástroj máte, stačí ověřit jeho funkčnost podle posledního kroku.

## 1. Visual Studio Code

Stáhněte a spusťte [instalátor Visual Studio Code pro Windows](https://code.visualstudio.com/download). Vyberte **User Installer** a ponechte zapnutou volbu **Add to PATH**.

## 2. Git

Stáhněte a spusťte [Git for Windows](https://git-scm.com/install/windows). Ponechte výchozí nastavení.

## 3. uv

Otevřete **PowerShell** z nabídky Start a spusťte tento příkaz z [oficiálního návodu uv](https://docs.astral.sh/uv/getting-started/installation/):

```powershell
powershell -ExecutionPolicy ByPass -c "irm https://astral.sh/uv/install.ps1 | iex"
```

## 4. Python pomocí uv

Zavřete a znovu otevřete PowerShell. Nainstalujte [Python pomocí uv](https://docs.astral.sh/uv/guides/install-python/):

```powershell
uv python install
```

## 5. Docker Desktop – na pozdější část kurzu

Stáhněte a nainstalujte [Docker Desktop pro Windows](https://docs.docker.com/desktop/setup/install/windows-install/). Ponechte zapnutou volbu **Use WSL 2 instead of Hyper-V**, pokud ji instalátor nabízí.

Pokud nemáte WSL, otevřete PowerShell **jako správce**, spusťte `wsl --install` a restartujte počítač. Pokud Docker požaduje aktualizaci WSL, spusťte `wsl --update`.

Spusťte **Docker Desktop** a počkejte na spuštění enginu. Instalaci můžete odložit, dokud Docker nebudeme v kurzu používat.

## 6. Registrace na GitHubu

Vytvořte si [bezplatný účet na GitHubu](https://github.com/signup) a ověřte e-mailovou adresu. Pokud účet už máte, ověřte, že se do něj můžete přihlásit.

## 7. Codex nebo Claude Code – aplikace a CLI

Vyberte produkt, který máte předplacený s přístupem ke kódovacímu agentovi. Nainstalujte jeho **desktopovou aplikaci i CLI** (verzi pro příkazový řádek). Stačí jedna z následujících variant.

::::alternatives
:::option{label="Codex"}
**Aplikace:** nainstalujte [ChatGPT pro Windows s režimem Codex](https://learn.chatgpt.com/docs/windows/windows-app). Přihlaste se účtem s předplatným a vyberte **Codex**.

**CLI:** v PowerShellu spusťte [oficiální instalátor](https://learn.chatgpt.com/docs/config-file/environment-variables):

```powershell
irm https://chatgpt.com/codex/install.ps1 | iex
```

V novém okně PowerShellu ověřte instalaci příkazem `codex --version`. Potom spusťte `codex` a zvolte přihlášení přes **ChatGPT** se stejným účtem jako v aplikaci.
:::
:::option{label="Claude Code"}
**Aplikace:** stáhněte a nainstalujte [Claude pro Windows](https://claude.com/download). Přihlaste se účtem s předplatným a otevřete záložku **Code**.

**CLI:** v PowerShellu spusťte [oficiální instalátor Claude Code](https://code.claude.com/docs/en/setup):

```powershell
irm https://claude.ai/install.ps1 | iex
```

V novém okně PowerShellu ověřte instalaci příkazem `claude --version`. Potom spusťte `claude` a přihlaste se účtem s předplatným **Claude**, který používáte v aplikaci.
:::
::::

## 8. Ověření instalace

Zavřete a znovu otevřete PowerShell. Postupně spusťte:

```powershell
uv --version
uv run python --version
git --version
```

Každý příkaz má vypsat verzi nástroje.

Pokud jste nainstalovali Docker, nechte Docker Desktop spuštěný a zadejte `docker version`. Výstup má obsahovat části **Client** i **Server**.

Pokud některý příkaz není rozpoznán ani v novém okně, pošlete lektorovi jeho znění a chybovou zprávu.
