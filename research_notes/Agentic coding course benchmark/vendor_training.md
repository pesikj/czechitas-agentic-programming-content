# Official vendor training and best-practice docs for coding agents (benchmark for a Czechitas beginner course)

Research date: 2026-10-07. All pages were fetched on this date unless marked otherwise. Labels: **[V]** means verified on an official page fetched today. **[I]** means inferred. **[S]** means from a secondary or aggregator source, not verified on the official page. **[N/A]** means not publicly stated on the page fetched.

Important structural change: OpenAI's Codex documentation has **moved**. `developers.openai.com/codex/...` URLs now return 308 redirects to `learn.chatgpt.com/docs/...` (seen for `/codex/windows` and `/codex/pricing`). Some old deep links now return 404, including `learn.chatgpt.com/docs/best-practices` and `learn.chatgpt.com/guides/best-practices.md`, even though the second one is listed in the site's llms.txt. Course materials should avoid hard-coding Codex doc URLs or should check them before every run. — [redirect observed from developers.openai.com/codex/windows](https://developers.openai.com/codex/windows); [learn.chatgpt.com llms.txt](https://learn.chatgpt.com/llms.txt)

## 1. Official courses and learning paths (catalogue)

### Takeaway
Every major vendor now offers free, short, self-paced or live introductory material. **None of it is aimed at non-programmers who also have to learn Git, a terminal and Python**, except OpenAI's one-hour "Codex for Beginners" livestream, which shows non-technical use cases. Vendor courses assume a working developer setup and teach the agent itself. A 25–30 h Czechitas course therefore has to add a foundations layer: terminal, Git, reading code, testing and deployment. Vendor courses can cover the agent-specific layer.

### Cited Findings

**Anthropic Academy (Skilljar)**
- The catalogue lists four Claude Code-related courses: *Claude Code 101*, *Claude Code in Action*, *Introduction to Agent Skills* and *Introduction to Subagents*. The catalogue page states no length, price or certificate details. [V] — [anthropic.skilljar.com](https://anthropic.skilljar.com/)
- **Claude Code 101**
  - Audience: "new developers and experienced engineers exploring AI coding agents for the first time." [V]
  - Prerequisites: basic familiarity with code editors and the command line, plus a Claude Pro, Max or Enterprise account or an API key. [V]
  - Registration is free and a completion certificate is issued. [V]
  - Modules: What is Claude Code; How it works; Your first prompt; Installing; Daily workflows (Explore → Plan → Code → Commit, context management, code review); Customizing (CLAUDE.md, subagents, skills, MCP, hooks); Quiz. [V]
  - Length and last-update date are not stated. [N/A] — [Claude Code 101](https://anthropic.skilljar.com/claude-code-101)
- **Claude Code in Action**
  - Has been repositioned toward long, unsupervised sessions ("Run long, hands-off Claude Code sessions you can trust"). [V]
  - Audience: developers who already use Claude Code for single prompts. [V]
  - Free, with a certificate. [V]
  - Modules: Steer the Work; Configure Claude (CLAUDE.md, verification skills, permission modes, hooks); Automate Repeat Work (routines, headless mode, GitHub Actions); Verify and Share (unsupervised runs, plugins); Quiz. [V]
  - Format is video plus interactive modules. Length and update date are not stated. [N/A] — [Claude Code in Action](https://anthropic.skilljar.com/claude-code-in-action)
  - [I] Older descriptions of this course as a general introduction are probably out of date. For beginners, Claude Code 101 is now the better fit.
- **Introduction to Agent Skills / Introduction to Subagents**
  - Short topic courses on building SKILL.md skills and on delegating to subagents. Details are not stated on the catalogue. [V/N/A] — [anthropic.skilljar.com](https://anthropic.skilljar.com/)

**OpenAI Academy**
- **Codex Bootcamp**: three live one-hour sessions held 2026-09-23 to 2026-10-07 at 10:00–11:00 AM PT. [V]
  - 101 covers agentic coding: scoping tasks, giving context, steering, reviewing changes.
  - 201 covers team workflows: shared context, approvals, skills, tool connections.
  - 301 covers advanced automation: sub-agents, permissions, the Codex SDK.
  - Audience: "developers and technical teams." [V]
  - Price and recordings are not stated on the page. [N/A] — [Codex Bootcamp](https://academy.openai.com/public/clubs/builders-etkn1/resources/codex-bootcamp-2026-09-23)
  - Search-result snippet: Builders who attend all five live sessions receive a completion certificate. [S, not seen on the page] — [OpenAI Academy search result](https://academy.openai.com/public/clubs/builders-etkn1/overview)
- **Codex for Beginners**: a one-hour livestream on 2026-04-21 for "anyone curious about building with AI, including those without technical experience." [V]
  - It demonstrates non-technical use cases and includes Q&A. A replay is available. [V] — [Codex for Beginners event](https://academy.openai.com/en/public/events/codex-for-beginners-wsz3p1tg0r)
- **Codex 101: Introduction and onboarding** (resource dated 2026-03-18) exists. Its contents were not fetched. [S] — [Codex 101 resource](https://academy.openai.com/public/clubs/builders-etkn1/resources/codex-101-introduction-and-onboarding-2026-03-18)
- OpenAI also publishes a docs-based learning hub at learn.chatgpt.com. It has guides, a CLI and IDE extension reference, and a weekly "What's new" digest. [V] — [learn.chatgpt.com llms.txt](https://learn.chatgpt.com/llms.txt)

**GitHub / Microsoft Learn**
- Microsoft Learn promotes four focused GitHub Copilot modules: [V]
  - [Copilot Spaces](https://learn.microsoft.com/en-us/training/modules/introduction-copilot-spaces/)
  - [Copilot coding agent](https://learn.microsoft.com/en-us/training/modules/github-copilot-code-agent/)
  - [Code review with Copilot](https://learn.microsoft.com/en-us/training/modules/code-reviews-pull-requests-github-copilot/)
  - [Agent mode](https://learn.microsoft.com/en-us/training/modules/github-copilot-agent-mode/)
- The same page points to GitHub certification exams and Microsoft "Applied Skills" assessments, including "accelerate app development using GitHub Copilot." The hub page is dated 2025-10-23, so it may be stale. [V] — [Microsoft Learn GitHub hub](https://learn.microsoft.com/en-us/training/topics/ignite/github)
  - Module durations were not fetched. [Gap]
- **GitHub Skills exercise "Build applications with Copilot agent mode"**: a template repository with a preconfigured Codespace in which learners build a small fitness app using agent mode. It takes "less than one hour." [S, via a learner's fork and secondary pages; skills.github.com itself was not fetched] — [fork of the exercise](https://github.com/FeiPengDev/skills-build-applications-w-copilot-agent-mode)

**Cursor**
- Cursor Learn is a free, web-based, docs-style course for developers. It covers AI fundamentals ("you are in control" of the trade-offs between time, money, reliability and effort) and practical patterns. [V]
  - Module list, length and certificate are not stated in the fetched content. [N/A] — [cursor.com/learn](https://cursor.com/learn)

**Google**
- Gemini CLI docs offer a quickstart and tutorials on file management, skills, sessions and automation. No formal course was found. [V] — [geminicli.com/docs](https://geminicli.com/docs/)
- **Major change:** the docs state "Unpaid tier and Google One users: Gemini CLI was replaced by Antigravity CLI on June 18th, 2026." [V] — [geminicli.com/docs](https://geminicli.com/docs/)
  - Secondary press: Antigravity 2.0 was announced at Google I/O on 2026-05-19. The free, AI Pro and AI Ultra individual tiers lost Gemini CLI access on 2026-06-18. Enterprise and paid-API users kept access. Antigravity CLI is not open source. [S] — [The Register](https://www.theregister.com/ai-ml/2026/05/20/bye-bye-gemini-cli-google-nudges-devs-toward-antigravity/5243605); [The New Stack](https://thenewstack.io/gemini-cli-antigravity-replacement/)

**Replit, Windsurf**: not researched within this budget. [Gap]

### Inferences
- [I] Vendor courses run about 1–3 hours each. They are free and come with a quiz or certificate. They are typically unversioned and undated, so a course cannot cite them as stable references.
- [I] Two topic sets recur across vendors and form a de facto "credible" core curriculum:
  - Claude Code 101: what an agent is, install, prompting, explore–plan–code–commit, context management, instruction files, skills, subagents, MCP, hooks.
  - Codex Bootcamp 101–301: scoping, context, steering, review, then approvals, skills, tools and sub-agents, then automation.

### Gaps
- Lengths, last-update dates and lab formats for most Skilljar, OpenAI Academy and Microsoft Learn items are not displayed publicly.
- Contents of Cursor Learn's modules, and any Replit or Windsurf learning tracks, were not verified.

## 2. Vendor-recommended workflow

### Takeaway
Anthropic and OpenAI recommend essentially the same loop:
1. Explore read-only.
2. Plan, ideally in plan mode, or write a spec.
3. Implement against an executable check: tests, a build, a linter or a screenshot.
4. Review the diff, ideally with a fresh-context reviewer.
5. Commit.

Anthropic says outright that the single most important practice is giving the agent a way to verify its work. Its second theme is managing the context window.

### Cited Findings
- **Claude Code best practices** — [code.claude.com/docs/en/best-practices](https://code.claude.com/docs/en/best-practices)
  - Most practices stem from one constraint: the context window fills quickly and performance degrades as it does. [V]
  - "Give Claude a way to verify its work" (tests, a build exit code, a linter, a screenshot compared with a design) is the first tip. The agent should iterate until the check passes and show evidence rather than just claiming success. [V]
  - Verification can be enforced at four strengths: in a single prompt, as a session `/goal`, as a deterministic Stop hook, or by a verification subagent acting as a second opinion. [V]
  - Four-phase workflow: Explore (plan mode, read-only) → Plan (editable plan, Ctrl+G) → Implement (write and run tests) → Commit (with a PR). Skip planning when the diff fits in one sentence. [V]
  - Visual verification: paste a design screenshot, have Claude screenshot its result, then list and fix the differences. [V]
  - Spec-first for larger features: have Claude interview you and write SPEC.md, then implement in a fresh session. A good spec names files, states what is out of scope and ends with an end-to-end verification step. [V]
  - TDD-style prompts appear: "write a failing test that reproduces the issue, then fix it." There is also a Writer/Reviewer split, where one session writes tests and another writes code. [V]
  - Session hygiene:
    - Correct early with Esc.
    - Rewind with checkpoints (Esc Esc or `/rewind`). Checkpoints do not cover Bash changes and do not replace Git.
    - Run `/clear` between unrelated tasks.
    - After two failed corrections, start a fresh session with a better prompt.
    - Use `/compact <focus>`. [V]
  - Listed failure patterns: the kitchen-sink session, correcting over and over, an over-specified CLAUDE.md, the "trust-then-verify gap," and infinite exploration. [V]
  - Adversarial review: before calling work done, have a subagent review the diff against PLAN.md, or run the bundled `/code-review`. Flag only gaps that affect correctness, to avoid over-engineering. [V]
- **Claude Code 101 course** teaches "Explore → Plan → Code → Commit" as its daily-workflows module. [V] — [Claude Code 101](https://anthropic.skilljar.com/claude-code-101)
- **OpenAI Codex Bootcamp 101** teaches scoping tasks, providing context, steering work and reviewing code changes. [V] — [Codex Bootcamp](https://academy.openai.com/public/clubs/builders-etkn1/resources/codex-bootcamp-2026-09-23)
- **AGENTS.md guidance**: agents run the test commands listed in the file. Typical sections are project overview, build/test commands, code style, security and deployment. [V] — [agents.md](https://agents.md/)
- OpenAI's dedicated Codex best-practices guide could not be fetched (404 after the docs migration). Its content is unverified. [Gap] — [listed in llms.txt](https://learn.chatgpt.com/llms.txt)

### Inferences
- [I] For the course, plan mode, test-driven verification, screenshot verification and "commit as a save point" are vendor-endorsed and tool-agnostic. They map directly to the course memory goals: Git as rollback, and "passing tests ≠ meeting the requirement."
- [I] The "fresh-context reviewer" pattern (subagent or second session) is a good teachable unit for advanced lectures. Both vendors support subagents.

### Gaps
- OpenAI's current written best-practice text was not verified because of the 404.

## 3. Cross-tool concepts: support matrix

### Takeaway
The concepts are now highly transferable:
- **Agent Skills (SKILL.md)** and **AGENTS.md** are open standards supported by Codex, Claude Code, Copilot/VS Code, Cursor and Gemini CLI.
- MCP, subagents, hooks, plan mode, sandbox/approval modes and compaction exist in most tools, under different names and commands.

Teach the concepts once and show the per-tool names in a lookup table.

### Cited Findings
- **AGENTS.md**
  - Stewarded by the Agentic AI Foundation under the Linux Foundation. [V]
  - Originated from OpenAI, Amp, Jules, Cursor and Factory. [V]
  - Supported by more than 25 tools, including OpenAI Codex, Google Jules, VS Code, GitHub Copilot, Cursor, Devin, Zed, Warp, Windsurf and Aider. [V]
  - Rules: plain Markdown with no required fields; the nearest file wins. [V] — [agents.md](https://agents.md/)
- **Claude Code reads AGENTS.md natively** from v2.1.277 when there is no CLAUDE.md. If a CLAUDE.md exists, only CLAUDE.md is read unless it imports `@AGENTS.md`. [V] — [Claude Code memory docs](https://code.claude.com/docs/en/memory)
  - [I] This is a recent change; older materials say Claude Code ignores AGENTS.md.
- **Claude Code memory**:
  - CLAUDE.md, written by you and loaded every session.
  - Auto memory, written by Claude: the first 200 lines or 25 KB are loaded each session, per repository.
  - `.claude/rules/` for path-scoped rules.
  - CLAUDE.local.md for personal settings.
  - Memory is advisory; use hooks for enforcement. [V] — [Claude Code memory docs](https://code.claude.com/docs/en/memory)
- **Agent Skills open standard**
  - Originally developed by Anthropic and released as an open standard. [V]
  - A skill is a folder with SKILL.md (name and description at minimum) plus optional scripts, references and assets. [V]
  - Skills load by progressive disclosure: discovery, then activation, then execution. [V]
  - Listed clients include Claude Code, Claude, ChatGPT & Codex, GitHub Copilot, VS Code, Cursor, Gemini CLI, JetBrains Junie, OpenCode, Goose, Amp, Kiro, Roo Code, Factory and Tabnine. [V] — [agentskills.io](https://agentskills.io/)
- **Codex docs** have dedicated pages for AGENTS.md and custom instructions, subagents (custom Codex agents), skills, MCP, hooks (running scripts or MCP tools during the lifecycle) and "Rules" (controlling which commands can run outside the sandbox). [V] — [learn.chatgpt.com llms.txt](https://learn.chatgpt.com/llms.txt)
- **Codex sandbox and approvals**: [V] — [Codex agent approvals & security](https://learn.chatgpt.com/docs/agent-approvals-security)
  - The default sandbox is `workspace-write`.
  - Approval policies are `on-request` (the default), `never` and `granular`. The old `untrusted` policy is retired.
  - Network access is off by default locally.
  - OS sandboxes: Seatbelt on macOS, bwrap with seccomp on Linux, and a native Windows sandbox or WSL2.
- **Claude Code permission modes**: [V] — [Claude Code security](https://code.claude.com/docs/en/security); [best practices](https://code.claude.com/docs/en/best-practices)
  - **Auto mode**, where a classifier model reviews actions, is now the default starting mode for terminal and VS Code sessions from v2.1.283.
  - Manual mode (asks before writes and commands), Accept Edits, Plan mode and dontAsk.
  - Optional OS-level sandboxing via `/sandbox`.
  - [I] This is a big recent change; older courses teach "approve every action" as the default.
- **Claude Code extensibility**: [V] — [best practices](https://code.claude.com/docs/en/best-practices)
  - Skills in `.claude/skills/`, invocable as `/name`.
  - Subagents in `.claude/agents/`.
  - Hooks in settings.json, which are deterministic, unlike advisory CLAUDE.md.
  - MCP via `claude mcp add`.
  - Plugins that bundle all of these.
  - Context commands: `/compact`, `/clear`, `/rewind`, `/btw`.
- **Gemini CLI** has GEMINI.md context files, sandboxing, Agent Skills, MCP and a read-only plan mode. [V] — [geminicli.com/docs](https://geminicli.com/docs/)
- **GitHub Copilot** has agent mode (in the IDE) and a coding agent (cloud, assigned via issues and PRs) as separate concepts. It supports Agent Skills and AGENTS.md. [V] — [MS Learn hub](https://learn.microsoft.com/en-us/training/topics/ignite/github); [agentskills.io](https://agentskills.io/); [agents.md](https://agents.md/)

**Support matrix.** ✓ means verified today with a source above. (✓) means listed by a third-party standard site but not verified on the vendor's own docs. ? means not verified.

| Concept | Claude Code | OpenAI Codex | GitHub Copilot (VS Code) | Cursor | Gemini CLI |
|---|---|---|---|---|---|
| Instruction file | ✓ CLAUDE.md, also reads AGENTS.md (v2.1.277+) | ✓ AGENTS.md | (✓) AGENTS.md; custom instructions | (✓) AGENTS.md; rules | ✓ GEMINI.md; AGENTS.md ? |
| Auto/learned memory | ✓ auto memory | ? | ? | ? | ? |
| Agent Skills (SKILL.md) | ✓ | ✓ | (✓) | (✓) | (✓) |
| MCP | ✓ | ✓ | ✓ (MS Learn "GitHub MCP Server" module, [S]) | ? | ✓ |
| Subagents | ✓ `.claude/agents/` | ✓ subagents / custom agents | ? | ? | ? |
| Hooks | ✓ | ✓ | ? | ? | ? |
| Plan mode | ✓ (Shift+Tab, `--permission-mode plan`) | ? (not verified) | ? | ? | ✓ plan mode |
| Sandbox | ✓ `/sandbox` (macOS, Linux, WSL2; **not native Windows**) | ✓ on all OSes incl. native Windows | ? | ? | ✓ |
| Approval/permission modes | ✓ auto / manual / acceptEdits / plan / dontAsk | ✓ on-request / never / granular, plus sandbox levels | ? | ? | ? |
| Context compaction | ✓ auto + `/compact` | ? | ? | ? | ? |
| Rewind/checkpoints | ✓ `/rewind` | ? | ? | ? | ? |

### Inferences
- [I] The transferable core for teaching: instruction file, skills, MCP, subagents, plan → implement → verify, and permission/sandbox levels. Vendor-specific details: command names, auto-mode classifiers, auto memory, plugin marketplaces and cloud agents.
- [I] A course repository can ship a single AGENTS.md that works for both Codex and Claude Code, as long as no CLAUDE.md is present.

### Gaps
- Model and effort selection, compaction and plan mode in Codex were not verified on the docs. Neither were the Copilot, Cursor or Windsurf feature names.

## 4. Windows support and VS Code

### Takeaway
Both Codex and Claude Code now run **natively on Windows from PowerShell**. WSL is optional for both. The key difference is sandboxing:
- Codex ships a native Windows sandbox; the elevated mode needs admin setup.
- Claude Code's sandbox is not supported on native Windows; it needs WSL2. Native Windows users therefore rely on permission modes.

### Cited Findings
- **Claude Code on Windows** — [Claude Code setup](https://code.claude.com/docs/en/setup)
  - Supported on Windows 10 1809+ and Windows Server 2019+. Shells: PowerShell, CMD, Bash, Zsh. [V]
  - Install in PowerShell with `irm https://claude.ai/install.ps1 | iex`. A CMD variant and WinGet (`winget install Anthropic.ClaudeCode`) also exist. No Administrator rights are needed. [V]
  - Git for Windows is optional. Without it, Claude Code uses its PowerShell tool for shell commands; with it, Git Bash serves as the Bash tool. [V]
  - Options table: native Windows has no sandboxing; WSL2 supports sandboxing; WSL1 does not. [V]
  - Native installs auto-update; WinGet installs do not. [V]
  - There is a Desktop app for Windows and a terminal guide for first-time terminal users. [V]
  - Security note: avoid WebDAV paths on Windows. [V] — [Claude Code security](https://code.claude.com/docs/en/security)
- **Codex on Windows** — [Codex Windows docs](https://learn.chatgpt.com/docs/windows/windows-sandbox) (redirected from developers.openai.com/codex/windows)
  - Available through the native ChatGPT desktop app, the CLI and the IDE extension. [V]
  - Windows 11 recommended; Windows 10 1809+ gets best-effort support. Requires winget. [V]
  - Two sandbox modes: "elevated" (preferred; uses dedicated low-privilege users and firewall rules; administrator-approved setup) and "unelevated" (an ACL-based fallback with weaker network isolation). [V]
  - Warns that full-access mode is not limited to the project directory. [V]
- **Codex Windows timeline** from What's new: [V] — [Codex What's new](https://learn.chatgpt.com/docs/whats-new.md)
  - The native Codex app launched on Windows in March 2026.
  - Computer Use for Windows apps arrived in May 2026.
  - The IDE extension is available on macOS and Windows.
- **IDE extensions**: [V]
  - Claude Code has a VS Code extension and a JetBrains plugin. — [Claude Code setup (uninstall section)](https://code.claude.com/docs/en/setup)
  - Codex has an IDE extension ("Use Codex beside your code and editor context"). — [llms.txt](https://learn.chatgpt.com/llms.txt)

### Inferences
- [I] For a Windows-majority beginner class, native PowerShell install is now viable for both tools. WSL adds setup cost and is not required.
- [I] If the course wants an OS-level sandbox on Windows, Codex offers one natively, though the elevated setup needs admin rights, which can be a problem on locked-down work laptops. Claude Code would need WSL2.

### Gaps
- Exact VS Code extension behaviour on Windows, for example whether the Claude Code extension uses PowerShell or Git Bash, was not verified.

## 5. Pricing and access for beginners (checked 2026-10-07)

### Takeaway
- **Codex is included in every ChatGPT plan, including Free and Go.** That makes it the lowest-cost entry point, but the low-tier limits are unpublished.
- **Claude Code requires a paid plan.** Claude Pro is listed at $25/month billed monthly or $17/month billed annually; the Free plan has no Claude Code.
- GitHub Copilot Free includes agent mode and CLI with limited usage.
- Gemini CLI's free tier ended in June 2026 (replaced by Antigravity CLI).

### Cited Findings
- **Codex plans and limits** — [Codex pricing](https://learn.chatgpt.com/docs/pricing)
  - Included in Free, Go, Plus, Pro, Business, Edu and Enterprise. [V]
  - Plus limits per 5-hour window, in local messages: GPT-6 Astra 5–45, GPT-6.1 Sol 15–160, GPT-6 Luna 350–3,000. Weekly limits may also apply. Local and cloud usage share one allowance. [V]
  - Pro has no 5-hour window limit. [V]
  - GPT-5.5 retires from Codex on 2026-10-14. [V]
  - Free and Go limits are not published on the page. [N/A]
  - The ChatGPT pricing page returned 403, so plan prices were not verified. [Gap] — [chatgpt.com/pricing](https://chatgpt.com/pricing)
- **Claude plans** — [claude.com/pricing](https://claude.com/pricing)
  - Free does not include Claude Code. [V]
  - Pro is "$17 per month with annual subscription discount ($200 billed up front), $25 if billed monthly," and includes Claude Code. [V]
    - [I] This looks like a price change from the widely cited $20/month; double-check before quoting it to learners.
  - Max starts at $100/month (5x or 20x Pro usage). [V]
  - Limits reset on a rolling 5-hour window, with no fixed message count. [V]
  - Setup docs confirm Claude Code needs a Pro, Max, Team, Enterprise or Console account. [V] — [Claude Code setup](https://code.claude.com/docs/en/setup)
- **GitHub Copilot** — [Copilot plans](https://github.com/features/copilot/plans)
  - Free: $0, "limited chat and agent usage," 2,000 completions per month, CLI and agent mode access. [V]
  - Pro: $10/month with $15/month in "GitHub AI Credits," plus a cloud agent. [V]
  - Pro+: $39/month with $70 in credits. [V]
  - Max: $100/month with $200 in credits. [V]
  - [I] The billing model has moved from "premium requests" to "AI Credits."
  - Student plan details were not shown in the fetched content. [Gap]
- **Gemini CLI**: unpaid-tier and Google One users were moved to Antigravity CLI on 2026-06-18. [V] — [geminicli.com/docs](https://geminicli.com/docs/)
- **Cursor free tier**: not verified. [Gap]

### Inferences
- [I] For a course where learners pay themselves, Codex on ChatGPT Plus (which many advanced ChatGPT users already have) or Free/Go for a trial is the cheapest path. Claude Code costs at least $17–25/month extra.
- [I] Copilot Free is a credible zero-cost fallback for learners without a subscription. It also needs a GitHub account, which the course teaches anyway.
- [I] Limits are expressed as ranges and shared across local and cloud use. Heavy in-class sessions on Plus could hit the 5-hour cap on the top model. Teach model and effort selection, using the cheaper model for routine work.

### Gaps
- Codex limits on Free and Go, Copilot Student, Cursor Hobby, and ChatGPT Plus and Go prices were not verified.

## 6. Vendor security guidance

### Takeaway
Vendors give three consistent messages:
1. Keep the agent inside the project with sandbox and permission modes, and treat "full access / never ask" as dangerous.
2. Network access and web content are the main prompt-injection vector.
3. The human is responsible for reviewing commands and diffs.

Secrets guidance is thin in the official docs.

### Cited Findings
- **Claude Code** — [Claude Code security](https://code.claude.com/docs/en/security)
  - The user is "responsible for reviewing proposed code and commands for safety before approval." [V]
  - Prompt-injection protections: [V]
    - Approval is required for network commands such as curl and wget.
    - Web pages are summarised by a separate model call.
    - A workspace trust dialog appears for new folders.
    - Project `.mcp.json` servers have their own approval prompt.
    - Commands that cannot be analysed require approval.
    - Matching is fail-closed.
  - Best practices for untrusted content: review commands, avoid piping untrusted content in, check edits to critical files, use VMs for risky work, report with `/feedback`. [V]
  - MCP: only use servers you trust. Anthropic reviews directory connectors but "does not security-audit or manage any MCP server." [V]
  - Credentials are stored in the macOS Keychain, in a 0600 file on Linux, and in the user-profile ACL on Windows. [V]
  - There is a `/security-review` command and a security-guidance plugin. [V]
  - The working-directory boundary is a prompt, not OS isolation. An approved Bash command can write anywhere unless the sandbox is on. [V]
- **Codex** — [Codex agent approvals & security](https://learn.chatgpt.com/docs/agent-approvals-security); [Codex Windows docs](https://learn.chatgpt.com/docs/windows/windows-sandbox)
  - The workspace-write sandbox is the default. Network is off by default. Web search defaults to "cached" mode to reduce prompt-injection risk. [V]
  - Warning: "Prompt injection can cause the agent to fetch and follow untrusted instructions." [V]
  - Cloud secrets are available only during setup and are removed before the agent phase. [V]
  - Asynchronous safety monitoring can pause tasks, but supplements rather than replaces the sandbox. [V]
  - Full-access mode can perform destructive actions outside the project. [V]
- **AGENTS.md** recommends a "security considerations" section in the instruction file. [V] — [agents.md](https://agents.md/)

### Inferences
- [I] Beginner-relevant security lessons:
  - Never run in full-access or bypass mode.
  - Keep `.env` out of Git and out of prompts.
  - Be wary of instructions inside web pages, issues or READMEs.
  - Review every diff before committing.
  - Add only trusted MCP servers.
  - These pair naturally with the course's Git and review goals and with deployment (secrets in the hosting provider's environment variables).

### Gaps
- No dedicated official "secrets handling for local agents" page was found for either vendor within budget.

## 7. Rate of change and implications for course maintenance

### Takeaway
These tools change **daily (Claude Code) or weekly (Codex)**, and documentation URLs, defaults, models, pricing and even product availability (Gemini CLI) shifted in the last six months. A 10-lecture course needs version-pinned screenshots, a "verified on date X" stamp per lecture, and a pre-cohort re-check pass.

### Cited Findings
- **Claude Code releases** shipped almost daily: 2.1.285 on 2026-09-29 through 2.1.292 on 2026-10-06, with two releases on 2026-10-06. [V] — [Claude Code changelog](https://code.claude.com/docs/en/changelog)
  - There is a "stable" channel, typically about one week behind "latest," that skips releases with major regressions. [V] — [Claude Code setup](https://code.claude.com/docs/en/setup)
- **Recent behaviour changes in Claude Code**: [V] — [best practices](https://code.claude.com/docs/en/best-practices); [memory](https://code.claude.com/docs/en/memory)
  - Auto mode became the default starting permission mode (v2.1.283).
  - Native AGENTS.md reading arrived in v2.1.277.
- **Codex "What's new"** is a weekly digest. Recent weeks introduced GPT-6 Astra (Aug 31–Sep 4), GPT-6 Sol and Luna (Sep 21–25), a GPT-5.5 retirement notice (Sep 14–18), GPT-6.1 Sol (Sep 28–Oct 2) and DevDay 2026 announcements. Codex CLI is at 0.147.0. [V] — [Codex What's new](https://learn.chatgpt.com/docs/whats-new.md)
- **Codex docs migration**: developers.openai.com/codex now redirects to learn.chatgpt.com, and some deep links 404. [V] — see redirect note at top.
- **Gemini CLI**: free-tier access ended on 2026-06-18, about 3.5 months before this research date. [V] — [geminicli.com/docs](https://geminicli.com/docs/)
- **Anthropic's Claude Code in Action** course has been refocused on long unattended sessions. [V] — [Claude Code in Action](https://anthropic.skilljar.com/claude-code-in-action)

### Inferences
- [I] Teach durable concepts (verify loop, plan mode, instruction files, skills, MCP, permissions, Git), not keystrokes. Keep tool-specific commands in a one-page appendix per tool that is refreshed before each run.
- [I] Pin learners to Claude Code's "stable" channel during a cohort to reduce surprises. For Codex, note the CLI version used in materials.
- [I] Model names (GPT-6.x, Claude) and plan limits should never be hard-coded into lecture text. Refer learners to the live pricing and usage pages instead.
- [I] Budget roughly one maintenance pass per cohort, plus an ad-hoc fix when a default changes (for example, the permission-mode default).

### Gaps
- No vendor publishes a deprecation schedule for course or tutorial content. Skilljar and OpenAI Academy pages show no "last updated" dates.
