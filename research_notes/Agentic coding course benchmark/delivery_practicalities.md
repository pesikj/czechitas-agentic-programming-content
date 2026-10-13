# Delivery practicalities for a beginner agentic-coding course (as of 2026-10-07)

All pages below were accessed on **2026-10-07**. "Verified" means the fact was read on the cited official page that day (through a fetch tool that summarizes pages, so exact wording can be lost). "Inferred" means my own reasoning from verified facts. Prices are in USD unless stated otherwise. I could not verify any Czech-localized (CZK/EUR incl. VAT) prices for AI subscriptions (see Gaps).

## 1. Free Django deployment options (with credit card requirements, sleep behaviour, SQLite persistence, limits)

### Takeaway
**Render Free** is the best main teaching target. It needs no card for the free tier, deploys from GitHub, and has a Django guide. Its drawbacks: the service sleeps after 15 minutes, the disk is ephemeral so SQLite data is lost on redeploy or restart, and the free Postgres expires after 30 days. **PythonAnywhere Free** is the best fallback and the only free option where SQLite stays on persistent storage. It has no Git auto-deploy, the web app must be renewed monthly, and outbound internet is limited to an allowlist. Fly.io, Koyeb, Cloud Run and Heroku all need a card. Hugging Face now requires a paid plan for Docker Spaces. Railway's free trial lasts only 30 days. Rule all of these out for a "no learner charge, no card" requirement.

### Cited Findings

**Render (verified)**
- Free web services spin down after 15 minutes with no inbound traffic, and waking up takes about 1 minute. Each workspace gets 750 free instance hours per month; when they run out, free services are suspended until the next month — [Render docs: Deploy for Free](https://render.com/docs/free)
- Free Postgres expires 30 days after creation, with a 14-day grace period before deletion. It is capped at 1 GB, with one free Postgres per workspace — [Render docs: Free](https://render.com/docs/free)
- Free services cannot attach persistent disks. There is no SSH, no scaling and no one-off jobs — [Render docs: Free](https://render.com/docs/free)
- The page does not say a card is required. It says that without a card on file, Render suspends services that exceed bandwidth or build-minute limits — [Render docs: Free](https://render.com/docs/free)
- The Django guide recommends replacing SQLite with managed Postgres. It uses `build.sh` to install dependencies and run migrations, gunicorn as the start command, WhiteNoise placed right after SecurityMiddleware, and the env vars `SECRET_KEY`, `DEBUG` (driven by the `RENDER` env var), `ALLOWED_HOSTS` from `RENDER_EXTERNAL_HOSTNAME`, and `DATABASE_URL`. A `render.yaml` Blueprint is optional — [Render: Deploy Django](https://render.com/docs/deploy-django)

**PythonAnywhere (verified)**
- The free "Beginner" plan includes one web app at `username.pythonanywhere.com`, 2 consoles, 100 CPU-seconds per day, 512 MB disk and no MySQL. Outbound internet is limited to "specific sites via HTTP(S) only" (allowlist). The cheapest paid tier, Developer, costs $10/month — [PythonAnywhere pricing](https://www.pythonanywhere.com/pricing/)
- The free web app has a "1 month expiry" — [PythonAnywhere help: Free account features](https://help.pythonanywhere.com/pages/FreeAccountsFeatures/)
- **Recent change:** for new users from 2026-01-08 (EU) and 2026-01-15 (US), unused web apps expire after 1 month instead of 3, scheduled tasks and MySQL moved to the paid tier, free accounts no longer get direct support, and the base paid tier went from $5 to $10 (€5 to €10 in EU) — [PythonAnywhere blog #221](https://blog.pythonanywhere.com/221/)
- Deploying an existing Django project is manual: `git clone` in a Bash console, create a virtualenv, create a web app with "Manual configuration", edit PythonAnywhere's WSGI file, map static files, then reload. The guide does not mention any GitHub auto-deploy — [PythonAnywhere: Deploy existing Django project](https://help.pythonanywhere.com/pages/DeployExistingDjangoProject/)
- Free web apps are extended by clicking a button on the Web tab ("Run until 3 months from today" in older material). Older sources describe a 3-month cycle — [PythonAnywhere blog #129](https://blog.pythonanywhere.com/129); this conflicts with the 1-month rule for new users in [blog #221](https://blog.pythonanywhere.com/221/)

**Railway (verified)**
- The free trial gives a one-time $5 credit valid for 30 days with no card required, up to 2 vCPU / 1 GB per service, 500 MB volumes and 7-day log retention. The ongoing Free plan gives $1/month of credit, 1 vCPU / 0.5 GB per service and 3-day log retention. The page does not say whether the Free plan needs a card — [Railway pricing](https://railway.com/pricing)

**Fly.io (verified)**
- New accounts get a trial of up to 2 hours of Machine runtime or 7 days, whichever ends first, with no card needed to start. "New organizations don't have a free tier or a monthly free usage allowance." All organizations (except Linked Organizations) need a card on file. The cheapest always-on machine costs $2.19 per 30 days. Legacy free allowances only apply to orgs on plans discontinued in October 2024 — [Fly.io pricing](https://docs.fly.io/about/pricing)

**Koyeb (verified)**
- One free instance per organization (512 MB RAM, 0.1 vCPU, 2 GB SSD), in Frankfurt or Washington D.C. only. It scales to zero after 1 hour without traffic and cannot use Volumes — [Koyeb instances](https://www.koyeb.com/docs/reference/instances)
- A card is required, verified with a $29 pre-authorization hold that is cancelled immediately. The old $5.50 credit has been discontinued — [Koyeb pricing FAQ](https://www.koyeb.com/docs/faqs/pricing)
- Free Postgres: "Free 5h" per month, 0.25 vCPU, 1 GB RAM, 1 GB storage — [Koyeb pricing](https://www.koyeb.com/pricing)

**Google Cloud Run (verified)**
- The free tier covers 180,000 vCPU-seconds, 360,000 GiB-seconds and 2 million requests per month. A billing account (card) is required even for the free tier — [Cloud Run pricing](https://cloud.google.com/run/pricing)

**Azure (verified)**
- App Service F1 is free: shared CPU with 60 CPU-minutes per day, 1 GB RAM, 1 GB storage, no SLA, and "intended for trials, experimentation, and learning" — [Azure App Service pricing (Linux)](https://azure.microsoft.com/en-us/pricing/details/app-service/linux/)
- Azure for Students gives a $100 credit for 12 months with no card required, but only to full-time university students verified by school email. It renews annually — [Azure for Students](https://azure.microsoft.com/en-us/free/students)

**Vercel (verified)**
- Django has zero-configuration support (detects `manage.py`). The app becomes a single Vercel Function on Fluid compute, `collectstatic` runs automatically and static files are served from the CDN, and WhiteNoise is only active locally. Vercel's own example falls back to SQLite only for local development and uses `DATABASE_URL` Postgres in production. The page is dated 2026-07-24 — [Vercel: Deploy Django](https://vercel.com/docs/frameworks/full-stack/django)

**Heroku (verified)**
- The GitHub Student Developer Pack gives $13/month for 24 months to students aged 18 or older, and requires a valid credit or debit card — [Heroku for GitHub Students](https://www.heroku.com/github-students/)

**Hugging Face Spaces (verified; recent change)**
- "Gradio and Docker Spaces run on compute and require a paid plan to create: PRO for personal accounts." Static Spaces are free. Free hardware sleeps when unused, and the disk is not persistent — [HF Spaces overview](https://huggingface.co/docs/hub/spaces-overview)

**Free Postgres (verified)**
- Neon Free is permanent with no card required: 1 GB per project (20 GB per account), 100 CU-hours per project per month, and scale-to-zero after 5 minutes. Writes are blocked when storage is exceeded — [Neon pricing](https://neon.com/pricing)
- Supabase Free: 500 MB database, 2 active projects, and projects pause after 1 week of inactivity. The page does not say whether a card is needed — [Supabase pricing](https://supabase.com/pricing)

### Inferences
- **Recommendation A (primary): Render Free + GitHub auto-deploy.** Teach two options. (a) Accept that SQLite resets on every deploy or restart, and seed demo data in the build step. (b) Better: connect a free Neon Postgres through `DATABASE_URL` (permanent, no card). Avoid Render's own free Postgres, which expires after 30 days and could vanish in the middle of a 10-lecture course.
- **Recommendation B (fallback / "persistent SQLite" demo): PythonAnywhere Free.** SQLite on its disk persists, so it is the simplest mental model. The manual WSGI setup is a good learning moment but adds friction. Learners must renew the app monthly, and the outbound allowlist may block external APIs the app calls.
- Railway's no-card trial ($5, 30 days) is fine for a single lecture demo but expires during the course.
- Vercel works for Django only with an external database. Serverless functions have no writable persistent disk, so SQLite does not persist there (inferred from the docs' SQLite-only-locally pattern; Vercel's filesystem limits page was not fetched). It suits the React frontend of the FastAPI+React transfer repo better.
- Hugging Face, Fly.io, Koyeb, Cloud Run, Heroku and Azure (non-student) are not suitable under the "no card, no charge" rule.
- Both Render and PythonAnywhere expose logs in their dashboards: the Render service "Logs" tab, and the PythonAnywhere error and server logs linked from the Web tab. This is based on general product knowledge and was not verified on a page this session.

### Gaps
- I did not verify whether Render requires a card at signup for the free tier. The docs only describe the suspension behaviour without a card.
- I did not get exact Render free instance specs (RAM/CPU) or Hobby plan pricing, because the pricing page did not render.
- I did not verify the PythonAnywhere outbound allowlist URL or confirm that GitHub (`github.com`) is on it. It historically is, which matters for `git clone`.
- I did not check Netlify for Django (only Vercel) or Azure F1 behaviour such as sleeping or "Always On".
- I could not confirm whether Railway's ongoing Free plan needs a card.

## 2. Teaching implications (SQLite on PaaS, static files, env vars, migrations, logs)

### Takeaway
A deployment lecture should cover five concepts. (1) The PaaS disk is ephemeral, so SQLite there is a demo, not storage. (2) Use WhiteNoise for static files. (3) Read `SECRET_KEY`, `DEBUG`, `ALLOWED_HOSTS` and `CSRF_TRUSTED_ORIGINS` from environment variables. (4) Run migrations in the build or pre-deploy step. (5) Read the platform logs when something fails. Django's `check --deploy` gives an automated checklist that the agent can run and explain.

### Cited Findings
- `SECRET_KEY` must be random and never committed. Load it with `os.environ["SECRET_KEY"]`. `DEBUG` must be `False` in production because it leaks source and settings. `ALLOWED_HOSTS` is required when `DEBUG=False`. Run `collectstatic` with `STATIC_ROOT` set. Set `CSRF_COOKIE_SECURE` and `SESSION_COOKIE_SECURE` to True under HTTPS. Run `python manage.py check --deploy`. The page documents Django 6.1 — [Django deployment checklist](https://docs.djangoproject.com/en/stable/howto/deployment/checklist/)
- Render's guide puts migrations in `build.sh`, places WhiteNoise right after SecurityMiddleware, and derives `ALLOWED_HOSTS` from `RENDER_EXTERNAL_HOSTNAME` — [Render: Deploy Django](https://render.com/docs/deploy-django)
- Render Free has no persistent disks — [Render docs: Free](https://render.com/docs/free). Hugging Face Spaces disk is "not persistent" — [HF Spaces overview](https://huggingface.co/docs/hub/spaces-overview). Koyeb's free instance cannot use Volumes — [Koyeb instances](https://www.koyeb.com/docs/reference/instances)
- Vercel runs `collectstatic` automatically and serves static files from its CDN. It recommends `.env.local` for local env vars and never committing that file — [Vercel: Deploy Django](https://vercel.com/docs/frameworks/full-stack/django)

### Inferences
- A good teaching pattern: run SQLite locally and use `DATABASE_URL` (via `dj-database-url`, or the plain `urllib` parse shown in Vercel's docs) in production. This teaches environment-specific configuration in one small change.
- `CSRF_TRUSTED_ORIGINS` (with the `https://` scheme) is a common cause of 403 errors on admin or form POSTs behind a PaaS domain. This is general Django knowledge; the checklist page summary did not explicitly confirm it.
- A good "intentional failure" exercise: deploy with `DEBUG=False` and no `ALLOWED_HOSTS`, get a 400 error, read the logs, and fix the setting with the agent.

### Gaps
- I did not verify the platform-specific log UIs or the Render "pre-deploy command" availability on Free.

## 3. Setup across Windows, macOS and Linux

### Takeaway
On Windows, Python installation changed in 2025–26. The recommended route is now the **Python Install Manager** (Microsoft Store or MSIX from python.org); the classic full installer is deprecated since 3.14 and will not ship for 3.16+. **uv** can fetch Python by itself and avoids many PATH and venv-activation problems, at the cost of one more tool to learn. Both Claude Code and Codex now run **natively on Windows without WSL**. Claude Code installs with a PowerShell one-liner and optionally uses Git for Windows. Codex has a native Windows sandbox and recommends its desktop app. Codespaces (120 hrs/month free on personal accounts) is a realistic fallback for broken laptops, but desktop-app agents do not run there.

### Cited Findings
**Python / uv**
- The recommended Windows install is the Python Install Manager, from the Microsoft Store (ID 9NQ7512CXL7T) or an MSIX on python.org. Commands: `python`, `py`, `pymanager`, e.g. `py install 3.14`. The full installer and `py.exe` launcher are deprecated since 3.14, and the full installer will not be produced for 3.16+. PATH entry: `%LocalAppData%\Python\bin`. If commands fail, check "Manage app execution aliases" — [Python docs: Using Python on Windows (3.14.8)](https://docs.python.org/3/using/windows.html)
- Activating a venv in PowerShell may need `Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope CurrentUser` so `Activate.ps1` can run — [Python venv docs](https://docs.python.org/3/library/venv.html)
- Install uv on Windows with `powershell -ExecutionPolicy ByPass -c "irm https://astral.sh/uv/install.ps1 | iex"` or `winget install --id=astral-sh.uv -e`; on macOS/Linux with `curl -LsSf https://astral.sh/uv/install.sh | sh` — [uv installation](https://docs.astral.sh/uv/getting-started/installation/)
- "By default, uv will automatically download Python versions when they are required." Python does not need to be installed separately; `uv python install 3.12` is available — [uv: Installing Python](https://docs.astral.sh/uv/guides/install-python/)

**Claude Code**
- Supported on Windows 10 1809+, macOS 13+, Ubuntu 20.04+ and Debian 10+ with 4 GB+ RAM. Shells: Bash, Zsh, PowerShell or CMD — [Claude Code setup](https://code.claude.com/docs/en/setup)
- Native install: on Windows PowerShell `irm https://claude.ai/install.ps1 | iex`, a CMD variant, or `winget install Anthropic.ClaudeCode` (no auto-update); on macOS/Linux `curl -fsSL https://claude.ai/install.sh | bash`. npm (`npm install -g @anthropic-ai/claude-code`) needs Node.js 22+ and is optional. No Administrator rights are needed — [Claude Code setup](https://code.claude.com/docs/en/setup)
- Git for Windows is optional but recommended (it provides Git Bash for the Bash tool). Without it, Claude Code uses the PowerShell tool. Sandboxing is not supported on native Windows and is supported on WSL 2. The docs list common beginner errors (PowerShell vs CMD confusion, `claude` not found on PATH) and include a `claude doctor` diagnostic. A desktop app is offered for people who prefer not to use the terminal — [Claude Code setup](https://code.claude.com/docs/en/setup)
- Claude Code requires a Pro, Max, Team, Enterprise or Console account. The free claude.ai plan does not include it — [Claude Code setup](https://code.claude.com/docs/en/setup)

**Codex**
- Windows options: the native ChatGPT desktop app (recommended; includes worktrees, Git, a built-in browser, plugins and skills), native PowerShell with a Windows sandbox (elevated or unelevated modes; no WSL/VM needed), and the CLI or IDE extension. Windows 11 is recommended; Windows 10 1809+ works "with reduced reliability". The setup typically needs `winget` — [Codex Windows sandbox docs](https://learn.chatgpt.com/docs/windows/windows-sandbox)
- CLI standalone installer: `curl -fsSL https://chatgpt.com/codex/install.sh | sh`. npm, Homebrew and Windows installs are also listed. Permission modes are set via `/permissions`: read-only, auto (edits and runs commands without confirmation), and full access — [Codex CLI docs](https://learn.chatgpt.com/docs/cli). Note: the developers.openai.com/codex URLs now redirect (HTTP 308) to learn.chatgpt.com, which is a recent docs relocation.

**Other tools**
- Gemini CLI installs via `npm install -g @google/gemini-cli` or `npx @google/gemini-cli`, so it needs Node.js — [Gemini CLI GitHub](https://github.com/google-gemini/gemini-cli)

**Codespaces / fallback**
- Personal GitHub Free accounts get 15 GB-month storage and "120 hrs" compute per month; Pro gets 20 GB-month and 180 hrs. Hours are counted as 2-core equivalents (a 4-core machine uses them twice as fast). Overage costs $0.18/hr (2-core) and $0.07/GB-month — [GitHub Codespaces billing](https://docs.github.com/en/billing/concepts/product-billing/github-codespaces)

### Inferences
- **Recommended Windows stack:** Git for Windows, VS Code, uv (which brings Python), the agent's native installer, and Node.js LTS only when the React lab arrives. Using uv (`uv run python manage.py runserver`) avoids `Activate.ps1` execution-policy errors altogether. If plain venv is taught instead, include the `Set-ExecutionPolicy RemoteSigned -Scope CurrentUser` step in the setup checklist.
- WSL is not required for either Claude Code or Codex. Avoid it for beginners; it doubles the filesystem and PATH confusion.
- Typical failure modes and fixes:
  - Microsoft Store `python` alias stub ("python not found" / opens the Store): check app execution aliases or use uv.
  - PATH not refreshed: open a new terminal.
  - PowerShell vs CMD confusion: the Claude docs explicitly list this error.
  - Corporate laptops without admin rights: the native installers need no admin.
  - Antivirus or managed policy blocking `irm | iex`.
  - Old Windows 10 builds.
  - OneDrive-synced Documents folder (an inferred risk, not verified).
- Mitigations: a pre-course setup session and a checker script (e.g., `git --version`, `uv --version`, `uv run python -V`, `claude --version` / `codex --version`, `node -v`, and `claude doctor`).
- Codespaces as a fallback: 120 hrs on a 2-core machine is enough for 10 lectures × 3h plus homework, assuming the default 2-core machine (inferred). CLI agents (Claude Code, Codex CLI) can be installed inside a Codespace terminal (inferred; not verified on a page).

### Gaps
- The Codespaces figure is ambiguous. The fetched table says "120 hrs", while historical GitHub docs said "120 core hours" (= 60 hrs on 2-core). Re-check the live page before relying on it.
- I did not verify Node.js current LTS version and Windows installer behaviour, VS Code install specifics, or GitHub Student Developer Pack Codespaces benefits.
- I did not verify a Codex npm install command or its Node version requirement.

## 4. Learner cost scenarios

### Takeaway
The cheapest viable paid agent options are **ChatGPT Plus ($20/mo)** for Codex and **Claude Pro ($20/mo, $17/mo annual)** for Claude Code. Both share limits across chat and coding. Free paths exist but are weaker or unstable:
- Codex in the ChatGPT desktop app on Free and Go "subject to rollout".
- Copilot Free with limited chat and agent usage.
- Gemini CLI free tier (1,000 requests/day).

Copilot has moved to "AI credits" billing, which is a recent change. I could not verify Czech VAT-inclusive prices.

### Cited Findings
**OpenAI / Codex (verified on learn.chatgpt.com; chatgpt.com/pricing and help.openai.com returned HTTP 403)**
- Free ($0) and Go ($8/mo): Codex "GPT-6 Luna at Standard speed in the desktop app, subject to rollout". No numeric limits are published — [Codex pricing](https://learn.chatgpt.com/docs/pricing)
- Plus ($20/mo): Codex on web, CLI, IDE extension and iOS. Local messages per 5-hour window: 350–3,000 with GPT-6 Luna, 15–160 with GPT-6.1 Sol. Extra credits can be purchased — [Codex pricing](https://learn.chatgpt.com/docs/pricing)
- Pro: from $100/mo ($100/$200/$500 options). "No five-hour limit on Pro plans". The $500 tier adds "Astra Ultrafast" — [Codex pricing](https://learn.chatgpt.com/docs/pricing)
- Business: $20/user/mo annual or $25 monthly, with the same 5-hour ranges as Plus. Edu/Enterprise: contact sales — [Codex pricing](https://learn.chatgpt.com/docs/pricing)
- Credit rates per 1M tokens (input / cached / output): Luna 2.5 / 0.25 / 12.5; Sol 50 / 2.5 / 250; Astra 250 / 25 / 1,250 — [Codex pricing](https://learn.chatgpt.com/docs/pricing)

**Anthropic / Claude Code**
- Pro costs $20/mo monthly or $17/mo billed annually and includes Claude Code. Max 5x costs $100/mo. Claude Code is in all paid plans, with usage shared across web, desktop, mobile and Code — [Claude pricing](https://claude.com/pricing); [Claude Max](https://claude.com/pricing/max)
- Pro and Max limits are shared between Claude and Claude Code. Use `/status` to monitor them. The help article gives no numeric limits — [Claude support: Claude Code with Pro/Max](https://support.claude.com/en/articles/11145838-using-claude-code-with-your-pro-or-max-plan)
- Team Standard costs $20/seat/mo annual or $25 monthly — [Claude pricing](https://claude.com/pricing)

**GitHub Copilot (verified; recent change to "AI credits")**
- Free ($0): 2,000 inline suggestions per month, "limited chat and agent usage" as an allowance of AI credits. CLI and agent mode are supported — [Copilot plans](https://github.com/features/copilot/plans); [GitHub docs: Copilot plans](https://docs.github.com/en/copilot/get-started/plans)
- Pro: $10/mo, 1,000 base + 500 flex credits (shown as "$15/month" of credits). Pro+: $39/mo, 3,900 + 3,100 credits. Max: $100/mo, 10,000 + 10,000 credits — [GitHub docs: individual plans](https://docs.github.com/en/copilot/concepts/billing/individual-plans). The two GitHub docs pages give Max as 20,000 credits total, which is consistent across them.
- Copilot Student gives verified students the full feature set for free. Verified teachers may get Pro for free — [GitHub docs: Copilot plans](https://docs.github.com/en/copilot/get-started/plans)

**Free alternatives**
- Gemini CLI with a personal Google login: 60 requests/min and 1,000 requests/day, with Gemini 3 models (1M context) — [Gemini CLI GitHub](https://github.com/google-gemini/gemini-cli)

### Inferences
- **Scenario A (lowest cost, uneven quality):** Copilot Free + Gemini CLI free = $0. Expect throttling mid-lab on Copilot Free. Gemini's 1,000 requests/day comfortably covers a 3h session (inferred).
- **Scenario B (recommended baseline):** one $20/mo plan (ChatGPT Plus or Claude Pro) for about 3 months of a 10-lecture course, roughly $60 total per learner before VAT. Czech VAT is 21%; if the vendor adds it on top, $20 becomes about $24.20/mo. This is not verified on a vendor page, and some vendors show VAT-inclusive local prices.
- **3h lab fit:** Plus allows 350–3,000 Luna messages per 5 hours, which should comfortably cover a 3h lab using the default/small model. With the Sol model (15–160 per 5h), heavy users could hit the limit mid-lab. Claude Pro publishes no numbers; anecdotally, heavy Claude Code use can exhaust a Pro 5-hour window, so plan "lighter model / smaller task" fallbacks (inferred, not verified).
- **Codex on Free/Go is "subject to rollout"** and desktop-app only, so it is not dependable for a whole cohort.
- Copilot Student is free and full-featured, but Czechitas learners are typically adults, not enrolled students, so most will not qualify (inferred).

### Gaps
- No CZK/EUR VAT-inclusive prices were verified for ChatGPT, Claude or Copilot. chatgpt.com/pricing returned 403, and claude.com showed only USD.
- **Claude Max 20x price is unverified.** The summarizer returned "$100" for both Max 5x and 20x, which is likely a "From $100" rendering artifact; historically 20x was $200. Confirm manually.
- The Copilot Free numeric credit allowance and premium-request limits for agent mode were not given on the pages fetched.
- I could not verify OpenCode free models, and I found no numeric Claude Pro 5-hour or weekly limits.
- The ChatGPT Go price ($8) is from the Codex pricing page; regional Go pricing may differ.

## 5. Security and teaching hygiene

### Takeaway
GitHub push protection for users is on by default and blocks known secret patterns pushed to **public** repos. Combine it with `.env` + `.gitignore` + env vars on the host. For agents, start beginners in approval or read-only modes before allowing auto-edit. Claude Code sandboxing is unavailable on native Windows, so approvals matter more there.

### Cited Findings
- Push protection for users "is enabled by default" and "stops you from pushing secrets to public repositories on GitHub". Bypassing it does not create alerts unless repo-level push protection is also on — [GitHub docs: About push protection](https://docs.github.com/en/code-security/secret-scanning/introduction/about-push-protection)
- Never commit `.env.local`; add it to `.gitignore` — [Vercel: Deploy Django](https://vercel.com/docs/frameworks/full-stack/django). `SECRET_KEY` must never be in source control — [Django checklist](https://docs.djangoproject.com/en/stable/howto/deployment/checklist/)
- Hugging Face warns Space owners when its secrets scanner finds hard-coded secrets, and separates public Variables from private Secrets — [HF Spaces overview](https://huggingface.co/docs/hub/spaces-overview)
- Codex permission modes (via `/permissions`): read-only, auto (edits and runs without confirmation) and full access. The Windows sandbox enforces "bounded filesystem and network permissions" — [Codex CLI](https://learn.chatgpt.com/docs/cli); [Codex Windows sandbox](https://learn.chatgpt.com/docs/windows/windows-sandbox)
- Claude Code sandboxing is "Not supported" on native Windows or WSL 1 and is supported on WSL 2 — [Claude Code setup](https://code.claude.com/docs/en/setup)

### Inferences
- Lecture 1 hygiene checklist:
  - Create `.gitignore` before the first commit (`.env`, `db.sqlite3`, `.venv/`, `__pycache__/`, `node_modules/`).
  - Generate `SECRET_KEY` per environment.
  - Store secrets in the Render/PythonAnywhere env-var UI only.
  - Have the agent run `git diff --staged` and review it before each commit.
- Start in "ask before edit / run" mode. Graduate to auto-edit inside a Git-tracked folder only after learners can use `git restore` / `git reset` to roll back.
- Learners' repos may be private, and push protection for users covers only public repos. Teach manual review regardless.

### Gaps
- I did not verify Claude Code's permission-mode names (default / acceptEdits / plan / bypass) on a page this session, or Codex's default mode on first run.
- I did not verify whether repository-level secret scanning is free for private personal repos.
