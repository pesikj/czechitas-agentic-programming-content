# Adjacent agentic-coding courses for experienced developers and CS students (benchmark for a beginner Czechitas course)

Research date: 2026-10-07. Verification labels: **[V]** verified from a primary source (course site, syllabus or repo fetched today); **[S]** from a secondary source or search-engine summary only; **[I]** my inference; **[N/A]** not publicly available. Courses primarily about building LLM apps or agent frameworks are excluded.

## 1. Which adjacent offerings exist, and which are strongest? (shortlist of 8)

### Takeaway
At least 8 credible offerings exist: 4 university courses with public syllabi (Stanford CS146S, UBC VSP "AI-Augmented Software Development + Studio", CMU 15-113/114, UMD CMSC 389A), 1 open curriculum (CRSS-AI Agentic SE), 1 vendor short course (DeepLearning.AI x Anthropic, Claude Code), 1 practitioner cohort course (Maven "Elite AI Assisted Coding"), and practitioner workshop or guide material (Simon Willison's NICAR 2026 handout and "Agentic Engineering Patterns"; Harper Reed and Addy Osmani workflows). The deep-dive picks are CS146S, UBC VSP26, CMU 15-113/114 and CRSS-AI. They have the most public material, and each has a different assessment model.

### Cited Findings
- **Stanford CS146S "The Modern Software Developer"**: instructor Mihail Eric. Fall 2026 is the second offering. The course description names "MCP, agent skills, spec-driven development, loop engineering, and the software factory". Prerequisite: "CS111/CS161 equivalent programming experience". The format is weekly lectures, hands-on coding, industry guest speakers and a final project. [V] — [themodernsoftware.dev](https://themodernsoftware.dev/)
- **CS146S assignments repo**: public, about 5.1k stars and 1.1k forks. It currently holds week1–week3 for Fall 2026; the last commit was 2026-10-05 ("Week 3 Assignment"). Setup uses Python 3.12, conda and Poetry. [V] — [GitHub mihail911/modern-software-dev-assignments](https://github.com/mihail911/modern-software-dev-assignments)
- **UBC Vancouver Summer Program 2026, "AI-Augmented Software Development + Studio"**: runs Jul 21–Aug 13, 2026 (4 weeks). Morning lectures run 09:30–11:50 and an afternoon studio runs 13:30–15:50 daily. Teams of 3–4 build and deploy a full-stack app. [V] — [ubc-vsp26.github.io](https://ubc-vsp26.github.io/)
- **CMU 15-113 / 15-114 "Effective Coding with AI"**: instructor Mike Taylor. 15-113 is a 7-week mini; 15-114 continues for another 7 weeks. The prerequisite is 15-112 (intro programming), with about 6 h/week. It uses free tools only (Gemini, Amazon Kiro, Claude, ChatGPT free tiers; VS Code/Kiro/Cursor). [V] — [cs.cmu.edu/~113](https://www.cs.cmu.edu/~113); prereq and hours from [CMU CSD course page](https://csd-web-01.andrew.cmu.edu/course/15113/s26) [S]
- **UMD CMSC 389A "Modern Software Development with GenAI"** (Fall 2026, Anwar Mamat): prereqs are CMSC216 and CMSC250. Students must buy Claude Code Pro ($20/month). Topics include Git, prompting, RAG, FastAPI, TDD and AI-generated tests, MCP, multi-agent, Docker/CI-CD, and security. [V] — [UMD syllabus](https://www.cs.umd.edu/class/fall2026/cmsc389A/Syllabus.html)
- **CRSS-AI "Agentic SE Course" (open curriculum)**: an "inverse classroom" with 5 weekly 1-hour live sessions plus an optional capstone. Developed March–April 2026 and last reviewed August 2026; last repo commit 2026-10-01. [V] — [GitHub CRSS-AI/agentic-se-course-early-2026](https://github.com/CRSS-AI/agentic-se-course-early-2026). The README links the full curriculum at [antonio-tresol.github.io/agentic-se-course-early-2026](https://antonio-tresol.github.io/agentic-se-course-early-2026/), while search lists [crss-ai.github.io/...](https://crss-ai.github.io/agentic-se-course-early-2026/), which returned only a title when fetched. [V]
- **DeepLearning.AI x Anthropic "Claude Code: A Highly Agentic Coding Assistant"**: taught by Elie Schoppik. Intermediate level, 1 h 50 min, 10 video lessons, 1 graded assignment. Three projects: exploring and extending a RAG chatbot codebase, refactoring a Jupyter notebook into a dashboard, and building a web app from a Figma mockup using MCP (Playwright, Figma). [S] (course pages returned 403; data from search snippets) — [deeplearning.ai course page](https://deeplearning.ai/short-courses/claude-code-a-highly-agentic-coding-assistant)
- **Maven "Elite AI Assisted Coding"**: Eleanor Berger (ex-Microsoft/Google). The current page lists 6 live sessions and 27 lessons at about 3–5 h/week; the next cohort is listed as the week of June 22. It is vendor-agnostic (Copilot, Claude Code, Codex, OpenCode, Cursor), with tiered homework (fundamentals vs stretch) completable in any language. Rated 4.6 from 89 reviews. Price was not shown on the fetched page. [V] — [maven.com/agentic-ventures/ai-coding](https://maven.com/agentic-ventures/ai-coding). An older listing describes a 3-week, 12-session format co-taught with Isaac Flath, covering AGENTS.md/plan.md/todos.md files, generic/curated/personalized context, parallel agents and spec-driven development. [S] — [maven.com/kentro/context-engineering-for-coding](https://maven.com/kentro/context-engineering-for-coding) (this URL returned 404 today, so the format has probably changed).
- **Simon Willison, NICAR 2026 "Coding agents for data analysis"**: a 3-hour workshop for data journalists, not developers. Modules cover setup, database querying, exploration, cleaning, visualization and scraping. It used GitHub Codespaces, offered a "YOLO mode" option or a local install, and worked with Claude Code and Codex. [V] — [NICAR 2026 handout](https://simonw.github.io/nicar-2026-coding-agents/). A search summary says a budget-restricted API key was distributed to attendees [S] — [simonwillison.net 2026/Mar/16](https://simonwillison.net/2026/Mar/16/); the fetched handout did not mention this (conflict, unresolved).
- **Simon Willison, "Agentic Engineering Patterns" guide**: chapters are designed to be updated over time rather than frozen. Chapters include Using Git with coding agents, Subagents, Red/green TDD, First run the tests, Agentic manual testing, Linear walkthroughs, Interactive explanations, Anti-patterns, and annotated prompts. [S] — [simonwillison.net/2026/Feb/23/agentic-engineering-patterns](https://simonwillison.net/2026/Feb/23/agentic-engineering-patterns/)
- **Harper Reed workflow**: idea honing (an LLM interviews you into `spec.md`), then planning (a reasoning model writes `prompt_plan.md` and `todo.md` as small test-driven steps), then execution step by step. [S] — [harper.blog 2025-02-16](https://harper.blog/2025/02/16/my-llm-codegen-workflow-atm/)
- **Addy Osmani workflow**: spec.md first, then a plan, then code. His Agent Skills pack has about 20 skills and 7 slash commands mirroring the lifecycle (/spec, /plan, /build, /test, /review, /code-simplify, /ship). [S] — [addyosmani.com/blog/ai-coding-workflow](https://addyosmani.com/blog/ai-coding-workflow/); [runtimewire](https://runtimewire.com/article/addy-osmani-agent-skills-claude-code-slash-commands)
- **Field survey**: an August 2026 arXiv paper (Geng, Shah, Denny, Leinonen, Griswold, Porter et al.) analyzes 23 public syllabi of upper-division credit courses on GenAI in SE. Only the abstract was checked; course names are not listed there. [V for abstract] — [arXiv 2608.05898](https://arxiv.org/abs/2608.05898)
- Other courses named only in a search summary: CMU "Effective Coding with AI", NJIT/Northeastern "AI-Assisted Software Engineering", UChicago "Design, Build, Ship", UIUC "Software Engineering with LLM Agents", Utah "Vibe Coding", UCSD "Generative AI and Programming", Michigan "Applied Agentic Software Engineering", Rochester "Software Design and AI-assisted Development" (Fall 2026). [S, unverified] — [search result incl. roclocality.org](https://roclocality.org/2026/03/21/software-design-and-ai-assisted-development-course-in-fall-2026/)

### Inferences
- [I] None of the verified offerings targets non-programmers learning to *build* software with agents. Willison's NICAR workshop is the closest, since it serves non-developers, but it focuses on data analysis. This supports the course's positioning as a gap.
- [I] The university courses converge on one topic list: context engineering, MCP, testing, security and review, deployment, and a team or capstone project. The beginner course's planned arc matches this list, so it is not idiosyncratic.

### Gaps
- Not checked: MIT, Berkeley, UW, TU Delft offerings; Frontend Masters, Egghead, Pluralsight AI-coding courses; Geoffrey Huntley workshop material. These were not reached within the tool budget, so they are neither confirmed nor ruled out.
- DeepLearning.AI lesson list, release date and price: the pages return 403, so these are unverified. The platform is usually free to audit, but that is not verified here.
- Maven price and current co-instructor: not verified.
- Codex-, Cursor- and Copilot-specific short courses: not researched.

## 2. In depth: Stanford CS146S. What are the structure, assignments and assessment?

### Takeaway
CS146S is the reference "AI-native SE" course. In Fall 2026 its assignments moved away from *using* an agent toward *dissecting and extending* one: trace a Claude Code session through a proxy, build an MCP server judged on "agent ergonomics", and author a skill tested on whether it triggers. All assignments use a points rubric and explicit deductions, for example for committed secrets.

### Cited Findings
- **Fall 2025 syllabus (10 weeks)** [S, secondary blog]:
  1. LLM foundations and prompting
  2. Agent architecture and MCP
  3. Context engineering and AI IDEs (guest from Cognition/Devin)
  4. Agent patterns and autonomy (Claude Code creator Boris Cherny)
  5. AI terminals (Warp CEO)
  6. Security and testing (Semgrep CEO)
  7. Code review (Graphite)
  8. Rapid app building (Vercel)
  9. Post-deployment operations (Resolve AI)
  10. Future of AI SE (Martin Casado)

  Grading was final project 80%, weekly assignments 15%, participation 5%. Fall 2026 runs Sep 22–Dec 3. — [heyuan110.com overview, 2026-02-24](https://www.heyuan110.com/posts/ai/2026-02-24-stanford-cs146s-overview/)
- **Fall 2026 Week 1, "Trace Dissection of a Real Claude Code Session"**: students run Claude Code against mitmproxy in reverse mode, using a project-level `.claude/settings.json` that sets `ANTHROPIC_BASE_URL`. The captured session must touch at least 2 files, fail at least once (breaking a test on purpose is suggested), produce an explicit plan, and run on the student's own scratch repo. Graded parts:
  - capture and reproducibility, 15
  - annotating the system prompt by "what behavior is this buying, and what failure mode is it defending against?", 25
  - tool inventory "numbers, not prose" plus interface analysis of 2 tools, 25
  - behavioral analysis, where every claim is labeled [OBSERVED] or [INFERRED] with cited evidence and unlabeled answers get no credit, 25
  - reflection, 10

  There are explicit sanitization rules (never paste headers; request bodies may contain `.env` contents) and deductions for unsanitized credentials. [V] — [week1/assignment.md](https://github.com/mihail911/modern-software-dev-assignments/blob/main/week1/assignment.md)
- **Week 2, "Build an MCP Server for a Third-Party API"**: at least 3 composing tools and at least 1 write tool. "Agent ergonomics" is 30 pts: constraints in the schema rather than prose, shaped output, errors as data, docstrings as contract, and a "brake" (dry_run or preview-then-commit) on write tools. A real OAuth flow with minimal justified scopes and no secrets in the repo (commit `.mcp.json.example`) is 25 pts. Integration requires a chained transcript, a demonstrated failure, and a protocol-level test. [V] — [week2/assignment.md](https://github.com/mihail911/modern-software-dev-assignments/blob/main/week2/assignment.md)
- **Week 3, "Author a Skill"**: pick a repeatable workflow with a real decision point and "run it manually once first" (15). Write a SKILL.md with a description that triggers, encoded judgment, exact commands and a lean body (60). Test it with 3 should-fire prompts plus 1 near-miss that should *not* fire, plus an end-to-end run on a chosen OSS repo such as htmx, dayjs or yt-dlp (25). Suggested skills include issue-to-plan, PR review against a rubric, bug reproduction, test writer, repo onboarding and security review. [V] — [week3/assignment.md](https://github.com/mihail911/modern-software-dev-assignments/blob/main/week3/assignment.md)
- Submission is a GitHub repo shared with staff plus Gradescope. Stanford provides Claude Code access through the student's SUNet ID. [V] — same repo

### Inferences
- [I] The week 1 trace assignment is too technical for beginners. Its core idea, *look at what the agent actually received and did*, can be adapted: for example, have learners read a session transcript or the `/context` view and annotate where the plan, the failure and the recovery happened, labeling claims observed vs inferred.
- [I] The week 3 near-miss trigger test is directly usable in the course's skills lecture.
- [I] The week 2 "brake on write tools" principle maps to teaching permission modes and dry-runs to beginners.

### Gaps
- The Fall 2025 per-week assignment specs and the Fall 2026 grading split were not verified from the primary site. The 80/15/5 figure comes from a secondary blog.
- The final project rubric is not public. Student work samples were not found.

## 3. In depth: UBC VSP26 "AI-Augmented Software Development + Studio". How is judgment assessed?

### Takeaway
UBC has the most explicit assessment philosophy for an agent-era course: "We do not grade AI-produced code; we grade your judgment about it." It pairs no-AI quizzes and judgment artifacts with a studio milestone that requires a CLAUDE.md, a test suite, a Semgrep scan, deployment and an AI usage log. The stack (FastAPI, Render, Neon) overlaps the beginner course.

### Cited Findings
- **Morning course grading**:
  - 11 proctored in-class quizzes with no AI, 5% each, two lowest dropped: 45%
  - "Judgment artifacts": A, an MCP tool-design specification (15%), and B, an "AI-output critique dossier" (15%): 30%
  - Ethics analysis of 600–900 words, with no AI permitted: 10%
  - Engagement: 15%

  [V] — [UBC VSP26 assessments](https://ubc-vsp26.github.io/assessments/)
- **Studio grading**:
  - M1 Foundation (skeleton, design doc, user stories, **CLAUDE.md**): 15%
  - M2 Integration (MCP integration, test suite, **Semgrep security scan**): 25%
  - M3 Ship It (deployed app, README, **AI usage log**, retrospective): 35%
  - Presentation: 15%
  - Peer evaluation: 10%

  The disclosure model is "transparency, not prohibition". [V] — [assessments](https://ubc-vsp26.github.io/assessments/)
- **Syllabus blocks**: Foundations (LLM mechanics, prompting, context engineering, agent architecture), Tooling and Workflow (MCP, AI IDEs, test evaluation), Building Real Systems (security, full-stack, code review), and Professional Practice. Test evaluation stresses "genuine coverage versus false confidence" and covers property-based and mutation testing concepts. By Session 4 the studio must have a working FastAPI backend, a DB and a minimal frontend. Tools: Claude Code, Cursor, Semgrep, GitHub, FastAPI, **Render, Neon**. [V] — [UBC VSP26 syllabus](https://ubc-vsp26.github.io/syllabus/)

### Inferences
- [I] A "critique dossier" (assess an agent's output and justify the verdict) is a strong beginner-compatible assessment. Grading the reasoning rather than the code fits learners who cannot yet write code.
- [I] The milestone requirements (CLAUDE.md, tests plus a security scan, then deploy plus an AI usage log) map almost one-to-one onto the planned lectures and could serve as the capstone checklist.
- [I] UBC also uses Render, which partially supports the deployment-provider direction in the course memory (free tier not verified here).

### Gaps
- The detailed brief or rubric for the critique dossier and the MCP spec artifact is not on the fetched pages. The syllabus page did not name them; only the assessments page did.

## 4. In depth: CMU 15-113/114 "Effective Coding with AI". How does it assess understanding of AI-written code?

### Takeaway
CMU's course is the closest in audience level: post-intro students on free tools. Its assessment design relies on **oral evaluations framed as mock job interviews**, **prompt logs**, **TA check-ins** and **reflections that students write themselves**, enforcing the rule that students must be able to explain any code they submit.

### Cited Findings
- **Grading**: homework 20%, participation 20%, big projects 30%, TA check-in meetings 10%, oral evaluations plus quizzes 20%. [V] — [cs.cmu.edu/~113](https://www.cs.cmu.edu/~113)
- **Projects**:
  - P1: a personal portfolio site (HTML/CSS/JS), which later projects are added to
  - P2: a deployed full-stack web app using APIs, a DB or data visualization
  - P3 (15-114 only): a portfolio-ready app with at least 2 advanced features

  Spec-driven planning before implementation is taught explicitly. [V] — same
- **AI policy**: document significant AI usage in code comments, explain generated code in your own words, and modify and test rather than copy-paste. "Submitting code you cannot explain" is prohibited, and instructors may ask students to explain code, trade-offs and alternatives. [V] — same
- The course describes students as collectively developing "evolving best practices" for future offerings. [S] — [CMU CSD course page](https://csd-web-01.andrew.cmu.edu/course/15113/s26)

### Inferences
- [I] A short "explain this diff to me" oral check, done instructor-to-learner or peer-to-peer, is a cheap, scalable verification format for a Czechitas course with no formal grading.
- [I] The portfolio-from-week-1 pattern suits career-switchers.

### Gaps
- Per-homework specifications and the oral evaluation rubric were not found publicly.

## 5. In depth: CRSS-AI open "Agentic SE Course". How does an agent-first curriculum handle workflow and tool change?

### Takeaway
This open curriculum treats the bottleneck as "ensuring that agent-produced code is correct, tested, coherent, and merge-ready". It sequences: one agent, then adapting it (skills, MCP, context), then Research-Plan-Implement, then harness engineering and multi-agent work, then a harness-first capstone. Its most transferable feature is the dated currency audit it keeps in the repo.

### Cited Findings
- **Structure**:
  - Week 0: install and live demo
  - Week 1: one coding agent
  - Week 2: skills, MCP, context engineering
  - Week 3: Research-Plan-Implement
  - Week 4: harness engineering and multi-agent coordination
  - Week 5 (optional): capstone built "harness-first"

  Pre-work is completed independently and followed by a 1-hour live session. [V] — [README](https://github.com/CRSS-AI/agentic-se-course-early-2026)
- **Week 3 pre-work** centres on Dex Horthy's "No Vibes Allowed" and the ACE-FCA write-up, plus Anthropic's Effective Context Engineering, large-codebases and dynamic-workflows docs, and Google's Conductor. **Reading checks** with answer keys test the talks through paired write-ups. [V] — [notes/curriculum-refresh-aug-2026.md](https://github.com/CRSS-AI/agentic-se-course-early-2026/blob/main/notes/curriculum-refresh-aug-2026.md)
- **Currency audit, 20 Aug 2026**: it checked link health (15 of 17 links return 200), publication-date errors, and items to prune that duplicate other items or have weak provenance (a pseudonymous gist). It flagged a feature doc (Agent Teams) as experimental and "disabled by default", so students following the note "will find that nothing happens". [V] — same file

### Inferences
- [I] The audit note is a reusable maintenance procedure for a course built on fast-moving tools: per-item verdict (keep, prune, annotate), date verification, and a check that each documented feature is actually enabled by default.

### Gaps
- The live-session exercises in the published site were not retrieved: one site URL returned only a title, and the other was not fetched.

## 6. Topic coverage across offerings (mention vs practice vs assessment)

### Takeaway
Mapping each topic to how deeply each offering treats it:

- **Assessed**: MCP, skills, context engineering, testing, security scanning and deployment, mainly at Stanford, UBC and UMD.
- **Taught but not assessed**: reading unfamiliar code (Stanford W3 OSS repos, DeepLearning.AI RAG codebase) and planning/specs (CRSS RPI, CMU spec-driven, Reed and Osmani). Reading unfamiliar code is assessed only indirectly.
- **Weakly covered**: cost/model selection, slopsquatting/supply chain, and "when to intervene". None of the fetched sources assessed them.

### Cited Findings
- **Context engineering / instruction files**: assessed at UBC (CLAUDE.md in M1) [V, [UBC](https://ubc-vsp26.github.io/assessments/)]; practiced at Maven (AGENTS.md, plan.md, todos.md) [S, [Maven](https://maven.com/kentro/context-engineering-for-coding)]; taught at CRSS Week 2 [V].
- **Skills**: assessed at Stanford W3, including trigger tests [V]; taught at CRSS W2 [V]; Osmani publishes a skill pack [S].
- **MCP**: assessed at Stanford W2 and UBC Artifact A/M2 [V]; practiced at UMD [V] and DeepLearning.AI (Playwright, Figma) [S].
- **Sub-agents / parallel work**: analyzed (trace evidence) at Stanford W1 [V]; taught at CRSS W4 [V]; covered at Maven (parallel agents) [S]; and in Willison's Subagents chapter [S].
- **Testing / TDD**: assessed at UMD ("evaluate AI-generated test suites for correctness and completeness") [V], at UBC (test suite in M2, "genuine coverage versus false confidence") [V], and at Stanford W2 (protocol-level test) [V]. Willison teaches Red/green TDD and "First run the tests" [S].
- **Security**: assessed at UBC (Semgrep scan in M2) [V] and Stanford (secret-handling deductions in W1/W2, minimal OAuth scopes) [V]. Fall 2025 W6 covered a Copilot RCE case study and OWASP [S]. Prompt injection and slopsquatting were not found explicitly in any fetched source.
- **Git / diff review**: Stanford 2025 W7 had code-review exercises on AI code [S]; UMD teaches Git/GitHub [V]; Willison has a "Using Git with coding agents" chapter [S].
- **Deployment**: required at UBC M3 (Render, Neon) [V] and CMU P2 [V]. Stanford 2025 W9 covered post-deployment operations [S].
- **Debugging agent failures / error recovery**: assessed at Stanford W1 (the captured session must include a failure, and recovery is quoted verbatim) and W2 (a demonstrated failure path) [V].
- **Independent verification**: Stanford W1 labels claims [OBSERVED]/[INFERRED] [V]; CMU uses orals [V]; UBC grades judgment [V].

### Inferences
- [I] Security topics the beginner course plans (permissions, secrets, prompt injection, slopsquatting) are under-taught even in advanced courses. Secrets hygiene, such as committing an `.example` config file and the Stanford sanitization rules, is the most mature pattern to borrow.
- [I] No course explicitly teaches "when to intervene" or cost/model selection, so the Czechitas course will need to design these itself.

### Gaps
- No fetched source documented cost/model-selection teaching or the prompt-injection/slopsquatting treatment.

## 7. Distinctive exercise and assessment designs worth adapting for beginners

### Takeaway
The best transferable designs all grade *judgment and evidence* rather than the code itself. They are listed with their sources below.

### Cited Findings
- **Forced-failure session**: the agent session must fail at least once, typically by deliberately breaking a test, so recovery can be studied. [V] — [Stanford W1](https://github.com/mihail911/modern-software-dev-assignments/blob/main/week1/assignment.md)
- **Observed vs inferred labeling**: claims without evidence labels earn zero, and mislabeling is penalized. [V] — Stanford W1
- **"Run it manually once first" before automating** a workflow into a skill, plus **near-miss trigger tests**. [V] — [Stanford W3](https://github.com/mihail911/modern-software-dev-assignments/blob/main/week3/assignment.md)
- **Brake on irreversible actions**: dry_run or preview-then-commit. [V] — [Stanford W2](https://github.com/mihail911/modern-software-dev-assignments/blob/main/week2/assignment.md)
- **AI-output critique dossier, and grading judgment rather than AI code**: [V] — [UBC](https://ubc-vsp26.github.io/assessments/)
- **Milestone checklist** (CLAUDE.md, then tests plus Semgrep, then deploy plus AI usage log plus retrospective): [V] — UBC
- **No-AI concept quizzes** alongside AI-permitted project work: [V] — UBC
- **Mock-interview orals and "can't explain it, can't submit it"**: [V] — [CMU](https://www.cs.cmu.edu/~113)
- **Prompt logs / AI usage logs**: [V] — CMU, UBC
- **Spec interview**: the LLM asks you questions one at a time to build `spec.md`, then `todo.md`. This fits ChatGPT power users. [S] — [Harper Reed](https://harper.blog/2025/02/16/my-llm-codegen-workflow-atm/)
- **Brownfield codebase tasks**: an existing RAG chatbot codebase [S, [DeepLearning.AI](https://deeplearning.ai/short-courses/claude-code-a-highly-agentic-coding-assistant)]; OSS repos for skills [V, Stanford W3].
- **Non-developer onboarding via cloud dev environments**: GitHub Codespaces in a 3-hour workshop. [V] — [Willison NICAR 2026](https://simonw.github.io/nicar-2026-coding-agents/)
- **Tiered homework** (fundamentals vs stretch) for mixed-ability cohorts: [V] — [Maven](https://maven.com/agentic-ventures/ai-coding)

### Inferences
- [I] **Deliberately flawed agent PRs** are not documented in any fetched source, although Stanford 2025 W7 "code review exercises for AI-generated code" may resemble them [S]. Seeding a Django PR with planted defects (a test that passes but misses a requirement, a hard-coded secret, an unrequested file change) would directly operationalize the course memory's point that "passing tests does not guarantee the requirement".
- [I] Codespaces could remove the Windows/PowerShell setup friction in the early lectures. This is a trade-off against the goal of learning local shell and Git.

### Gaps
- No public rubric for reviewing an agent's PR was found.

## 8. How do offerings handle rapid tool change?

### Takeaway
Three strategies appear:
- **Vendor-agnostic framing**: Maven; Stanford W3 grounds skills in the agentskills.io open standard.
- **Re-authoring every term**: Stanford rewrote its assignments between Fall 2025 and Fall 2026 and has students record `claude --version`.
- **Explicit currency audits and staleness disclaimers**: CRSS-AI, and Willison's guide chapters "designed to be updated".

### Cited Findings
- The Stanford Fall 2026 assignments (trace dissection, MCP plus OAuth, skill authoring) differ completely from Fall 2025's (prompting playground, MCP server, Warp task, etc.). [V for 2026, [repo](https://github.com/mihail911/modern-software-dev-assignments); S for 2025, [heyuan110](https://www.heyuan110.com/posts/ai/2026-02-24-stanford-cs146s-overview/)]
- The Stanford W1 writeup requires recording the Claude Code version. W3 points to the agentskills.io standard: "Claude Code, Cursor, and others all read the same format". [V] — repo
- The CRSS README says the course "might get outdated fast". The dated audit note shows link checks, date checks and feature-default checks. [V] — [CRSS repo](https://github.com/CRSS-AI/agentic-se-course-early-2026)
- Maven assignments are "tool-agnostic and completable in any programming language". [V] — [Maven](https://maven.com/agentic-ventures/ai-coding)
- Willison's guide format is a collection of chapters "designed to be updated over time, not frozen". [S] — [simonwillison.net](https://simonwillison.net/2026/Feb/23/agentic-engineering-patterns/)

### Inferences
- [I] For Czechitas, a reasonable approach is to teach the workflow (explore, plan, implement, verify, review, commit) as tool-agnostic. Add per-tool appendices (Claude Code vs Codex) that state the tested version, and run a pre-cohort audit modeled on the CRSS checklist.

### Gaps
- How DeepLearning.AI updates its video course as Claude Code changes is unknown (403).

## 9. Evidence of quality

### Takeaway
Quality evidence is uneven:
- **Strongest**: public, versioned assignment repos with rubrics (Stanford, about 5.1k stars).
- **Next**: public assessment schemes (UBC, CMU, UMD) and review ratings (Maven 4.6/89).
- **Missing**: student work samples and independent reviews.

### Cited Findings
- Stanford repo: about 5.1k stars, 1.1k forks; full rubrics in each assignment. [V] — [GitHub](https://github.com/mihail911/modern-software-dev-assignments)
- Maven: 4.6 rating from 89 reviews (platform reviews, not independent). [V] — [Maven](https://maven.com/agentic-ventures/ai-coding)
- A peer-reviewable survey of 23 syllabi exists (August 2026), useful as an external comparison. [V] — [arXiv 2608.05898](https://arxiv.org/abs/2608.05898)

### Inferences
- [I] Public rubrics, not enrollment numbers, are the most useful quality signal for adapting material.

### Gaps
- No public student projects or outcome data were found for any offering. Independent reviews were not located for DeepLearning.AI or Maven.
