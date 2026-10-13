# Make verification the graded core, not tools

*Research date: 2026-10-07. Based on five research-note files in `research_notes/Agentic coding course benchmark/` plus the local course memory, research brief and existing Czechitas web outline. Labels carried over from the notes: **[V]** verified on a primary source on the research date, **[I]** inferred, **[S]** secondary source only, **[NA]** not publicly available. Every competitor's lesson content is paywalled or locked, so no competitor's teaching quality was judged from its lessons; coverage claims rest on public syllabi, assignment repos and assessment pages.*

The Czechitas course can beat every comparable beginner offering found, but not by adding topics: it should win on **observable judgment**. The evidence shows that no beginner course visibly combines Python code reading, Git, testing on an existing codebase and deployment in a live cohort, and that no beginner course visibly uses seeded faults or assesses whether learners can catch an agent's mistakes ([Coursera – Build Apps with AI](https://www.coursera.org/learn/build-apps-with-ai); [ZTM](https://zerotomastery.io/courses/learn-vibe-coding/); [Czechitas Vibe coding v praxi](https://www.czechitas.cz/kurzy/vibe-coding-v-praxi-vytvor-si-vlastni-web-s-ai-bez-programovani)). The provisional outline already has the right ingredients but sequences them poorly: the agent's real workflow does not start until lecture 5, Git arrives after learners have already let an agent edit files, the FastAPI/React lecture adds a second language and a Node toolchain for a marginal transfer benefit, and advanced topics (skills, MCP, sub-agents) are crammed into one lecture as a tour. The seven most consequential changes are: compress two Python lectures into a reading kit plus recurring predict-run-investigate drills; put Git and safe permission modes before any autonomous editing; make acceptance criteria, criteria-coverage audits and seeded-fault reviews a graded ritual; thread security (secrets, prompt injection, hallucinated dependencies) through the course rather than mentioning it once; slim the transfer lecture to an unfamiliar Python API with a plain frontend; move instruction files early and keep only skills and a fresh-context reviewer hands-on in the advanced lecture; and assess with process logs, exit tickets and a five-minute capstone walkthrough. Evidence strength is uneven: the case for read-before-write pedagogy, for over-reliance risk and for verification gaps among non-developers is moderate and mostly transferred from university CS1 and professional studies, while the specific syllabus choices are curriculum-design judgment. A separate inconsistency needs an organizer decision now: the existing public web outline already requires ChatGPT Plus (Codex) and has three Python lectures, while the course memory records the agent budget as undecided.

## Seven changes outweigh any topic additions

The research converges on a single diagnosis. The market splits into tool-feature tours, which list CLAUDE.md, skills, MCP, hooks and sub-agents in a few hours of video, and "direct and verify" mental-model courses, which deliberately avoid Git and the terminal **[I]** ([Scrimba Claude Code on Coursera](https://www-cloudfront-alias.coursera.org/learn/introduction-to-claude-code); [Vanderbilt Build Apps with AI](https://www.coursera.org/learn/build-apps-with-ai)). Neither group visibly makes learners prove that an agent's work is right. Meanwhile the strongest pedagogical signal in the literature is that novices **know they should verify but do not**: a 2026 survey of 162 users found non-developers and novices aware of AI-code risks yet the least systematic verifiers, a "perception–action gap" ([Emergent Mind summary of arXiv 2605.24521](https://www.emergentmind.com/papers/2605.24521), secondary summary). CS1 students judged what LLM-generated code does correctly on only **32.5%** of tasks, with automation bias a named cause ([arXiv 2504.19037](https://arxiv.org/pdf/2504.19037)). An industry RCT with 52 developers found AI users scored about 50% versus 67% for hand-coders on a follow-up quiz, with the largest deficit on debugging, and that those who delegated code generation scored below 40% while those who asked conceptual questions scored at least 65% ([Anthropic research](https://www.anthropic.com/research/AI-assistance-coding-skills); [arXiv 2601.20245](https://www.arxiv.org/pdf/2601.20245)). ChatGPT power users arrive with exactly the delegation habit those studies link to weaker learning **[I]**.

The table below states each recommended change, why it matters, and how strong the supporting evidence is. "Moderate" means controlled studies or RCTs exist but on a different population (CS1, K-12, professionals) or with chat tools rather than autonomous agents; "Weak" means experience reports, surveys or practitioner consensus; "Design judgment" means no direct evidence and the recommendation is my reasoning from the constraints.

| # | Change | Rationale | Evidence strength |
|---|---|---|---|
| 1 | Replace the two front-loaded Python lectures with a compact "reading kit" (lectures 1–2, shared with setup, Git and first agent use) plus a 15–20-minute predict-run-investigate drill on agent output in every later lecture | Learners' main job is reading generated code; PRIMM and Parsons problems have controlled/quasi-experimental support; UCSD's CS1-LLM redesign reprioritised reading, testing and debugging with AI from week 1 and saw exam performance comparable to historical cohorts ([arXiv 2510.18806](https://arxiv.org/abs/2510.18806)) | Moderate for read-before-write; no study compares front-loaded vs integrated Python in an agent course (design judgment) |
| 2 | Make verification a graded ritual: acceptance criteria before prompting, criteria-coverage audit of agent-written tests, seeded-fault reviews, diff review before every commit | Perception–action gap; automation bias; LLM help raised student acceptance-criteria scores by 88% ([arXiv 2502.02675](https://arxiv.org/pdf/2502.02675)); both major vendors name verification as the top practice ([Claude Code best practices](https://code.claude.com/docs/en/best-practices)) | Moderate (mechanism well documented; no study of novices catching "tests pass but wrong requirement") |
| 3 | Put Git checkpoints and "ask before edit" permission modes in lecture 1–2, before any autonomous editing | Claude Code's checkpoints "do not replace Git" ([best practices](https://code.claude.com/docs/en/best-practices)); Claude Code's default starting mode became the classifier-based auto mode in v2.1.283, so beginners will start in a permissive mode unless taught otherwise ([Claude Code security](https://code.claude.com/docs/en/security)) | Vendor documentation [V]; ordering is design judgment |
| 4 | Thread security through lectures 1, 4, 6, 7 and the capstone: secrets, permissions, prompt injection, dependency existence | AI-assisted users wrote less secure code while believing it more secure ([arXiv 2211.03622](https://arxiv.org/abs/2211.03622v1)); 19.7% of LLM-recommended packages did not exist ([arXiv 2406.10279](https://arxiv.org/abs/2406.10279)); security is a single reading in Vanderbilt and absent from most beginner syllabi | Moderate (controlled study + large generation study; both from prior knowledge, URLs not re-fetched in notes) |
| 5 | Shrink the FastAPI/React lecture into a transfer lab on an unfamiliar small Python API with a pre-built plain HTML/JS frontend; React only as an optional demo | Keeps the authentic "get an unknown repo running" skill but avoids Node, npm and JSX for learners who are still learning to read Python; setup is the most reported novice barrier ([arXiv 2008.00315](https://arxiv.org/pdf/2008.00315); [arXiv 1712.05078](https://arxiv.org/pdf/1712.05078)) | Weak (experience reports) + design judgment |
| 6 | Move instruction files (AGENTS.md) to lecture 4; keep skills (with trigger tests) and a fresh-context reviewer hands-on in lecture 9; demonstrate MCP and parallel sub-agents only | AGENTS.md is a cross-tool open standard ([agents.md](https://agents.md/)); Stanford CS146S's skill assignment with "near-miss" trigger tests is adaptable ([week3](https://github.com/mihail911/modern-software-dev-assignments/blob/main/week3/assignment.md)); MCP server work is assessed only in developer courses | Vendor docs [V] + design judgment |
| 7 | Assess judgment, not output: process log per task, short exit tickets, two checkpoint reviews, a five-minute capstone walkthrough and a judgment-weighted rubric | UBC VSP26 states "We do not grade AI-produced code; we grade your judgment about it" ([UBC assessments](https://ubc-vsp26.github.io/assessments/)); CMU prohibits "submitting code you cannot explain" and uses oral evaluations ([CMU 15-113](https://www.cs.cmu.edu/~113)); code interviews are reported as authentic in intro courses ([arXiv 2410.01010](https://arxiv.org/html/2410.01010v2)) | Weak-to-moderate (design reports); no validated rubric exists for agentic-coding judgment |

Two further decisions are prerequisites rather than curriculum changes: run a pre-course setup clinic with a checker script, and decide the primary agent and learner budget so that the public web page, the course memory and the materials agree (see the final section).

## Ten beginner offerings exist, and none trains verification on real code

The research identified about ten beginner offerings, eight adjacent developer courses and a handful of vendor learning paths. The tables below include only offerings with enough public detail to compare; Udemy listings, Codecademy's one-hour Cursor lesson and DataCamp's self-ranked Replit course were found but excluded as too thin or self-promotional ([Codecademy](https://www.codecademy.com/learn/intro-to-ai-coding-with-cursor); [DataCamp blog](https://www.datacamp.com/blog/best-vibe-coding-course-for-non-technical-founders)). Prices and dates are as shown on 2026-10-07; "NA" means not publicly stated.

### Direct beginner competitors

| Provider / course | Audience | Prerequisites | Duration | Tools | Projects | Assessments | Price / access | Update date | Sources | Why selected |
|---|---|---|---|---|---|---|---|---|---|---|
| Vanderbilt (Jules White), *Build Apps with AI – From Idea to Working Product* (Coursera) | Beginners [V] | None stated beyond "Python or JavaScript" tools reading [V] | 6 h, 5 modules, self-paced [V] | Claude Code, Claude Cowork, MAJK, ChatGPT [V] | First web app; web app for own workflow [V] | 2 AI-graded builds; testing module ungraded [V] | Free enrolment, paid certificate [V] | NA | [Coursera](https://www.coursera.org/learn/build-apps-with-ai) | Strongest verification thinking in the beginner market ("Silent Failure Audit", user journeys → tests) |
| Scrimba, *Vibe Coding Essentials* specialization; component *Vibe Coding with Claude Code* (Coursera) | No coding experience (spec) [V]; component labelled **Intermediate** [V] | NA | 5 courses ≈15 h; Claude Code component 3 h, 25 videos [V] | Cursor, Copilot, Claude Code, MCP [V] | Portfolio, games, Chrome extensions, DB apps; Netlify deploy [V] | 2 assignments in Claude Code component [V] | Coursera subscription (exact price NA) | NA | [Specialization](https://www.coursera.org/specializations/vibe-coding); [Claude Code course](https://www-cloudfront-alias.coursera.org/learn/introduction-to-claude-code) | Most complete agent-mechanics coverage aimed at beginners; 22,397 enrolled |
| Zero To Mastery, *The Vibe Coding Bootcamp* | Complete beginners to experienced devs [V] | NA | 18 h video, 158+ lessons, 10+ projects [V] | Terminal, Node, Git, GitHub, VS Code, Copilot, Cursor, Zed, MCP, Ollama [V] | JS web projects; portfolio capstone [V] | NA | $299 course, $25/mo, $299/yr or $1,299 lifetime [V] | "Last updated October 2026" [V] | [ZTM](https://zerotomastery.io/courses/learn-vibe-coding/) | Only long beginner syllabus with a dedicated developer-setup module |
| Stanford Continuing Studies, TECH 36 A *Vibe Coding: Using AI for Programming* | Beginners and non-programmers [V] | None [V] | 5 × 1.5 h live (7.5 h) [V] | NA; learners told to expect $25–100/month tool costs [V] | NA | No grade (NGR) [V] | $455 [V] | Runs 24 Sep–22 Oct 2026 [V] | [Stanford CSP](https://continuingstudies.stanford.edu/courses/professional-and-personal-development/vibe-coding-using-ai-for-programming/20261_TECH-36-A) | Live cohort for non-programmers from a credible institution |
| Maven (Avthar Sewrathan), *Claude Code for Beginners: 2 Day Intensive* | Non-technical builders [V] | Claude Pro or Max [V] | ~6 h + 5 h live, office hours, Demo Day [V] | Claude Code, Skills, Plugins, MCP [V] | Own project to Demo Day [V] | Demo Day (no rubric visible) | Price NA | Cohort shown 14–15 March (year NA) | [Maven](https://maven.com/alpha-clarity/claude-code-for-beginners) | Representative live intensive; 4.9 from only 8 reviews |
| Vibe Code School, *Claude Code – Vibe Coding* | Zero coding experience [V] | None [V] | 28 lessons, 5 modules [V] | Claude Code [V] | 60-minute capstone [V] | NA | Free, no signup [V] | NA | [Vibe Code School](https://vibecodeschool.com/courses/claude-code-vibe-coding) | Topic list closest to ours, incl. "When to Interrupt" and legacy migration; single-author, low evidence [I] |
| DeepLearning.AI × Replit, *Vibe Coding 101* | Beginners [V via snippet] | None | ~1 h 34 min, 7 videos [V via snippet] | Replit cloud IDE | Performance analyzer; voting app [V via snippet] | 1 graded assignment (PRO) | Free / PRO (NA) | NA | [DeepLearning.AI](https://www.deeplearning.ai/short-courses/vibe-coding-101-with-replit/) (page returned 403) | Opposite setup trade-off: zero local install |
| **Czechitas, *Vibe coding v praxi*** (internal benchmark) | Non-programmers [V] | None [V] | 28 h, 6 sessions, 2 weeks [V] | Macaly (free PRO), Git, Vercel [V] | Own deployed web app [V] | Certificate at 80% attendance [V] | 21,990 CZK / 7,490 CZK discounted [V] | Run dated 29 Sep–10 Oct, year unconfirmed | [Czechitas](https://www.czechitas.cz/kurzy/vibe-coding-v-praxi-vytvor-si-vlastni-web-s-ai-bez-programovani) | Closest format match; the new course must be clearly differentiated from it |
| Engeto, *Web Developer Akademie* (Czech) | Career switchers | NA | 250+ h, 14–17 weeks [V] | Node, Express, PostgreSQL, Cursor [V] | Full-stack JS | NA | 25,990 CZK, possible 77% subsidy [V] | Next start 19 Nov 2026 [V] | [Engeto](https://engeto.cz/webova-akademie/) | Local market reference: traditional academy with AI, not agent-first |

### Adjacent developer courses (teaching-design sources, not competitors)

| Provider / course | Audience | Prerequisites | Duration | Tools | Projects | Assessments | Price / access | Update date | Sources | Why selected |
|---|---|---|---|---|---|---|---|---|---|---|
| Stanford CS146S *The Modern Software Developer* | CS students [V] | CS111/CS161-equivalent programming [V] | 10 weeks [V/S] | Claude Code, MCP, skills; Python 3.12 [V] | Weekly assignments + final project [V] | Points rubrics with explicit deductions (e.g. committed secrets) [V]; 2025 split 80/15/5 [S] | University credit; public assignment repo | Last commit 2026-10-05 [V] | [Course site](https://themodernsoftware.dev/); [assignments repo](https://github.com/mihail911/modern-software-dev-assignments) | Most public, versioned rubrics (~5.1k stars) |
| UBC VSP26 *AI-Augmented Software Development + Studio* | University students | NA | 4 weeks, daily lecture + studio [V] | Claude Code, Cursor, Semgrep, GitHub, FastAPI, Render, Neon [V] | Team full-stack app, deployed [V] | No-AI quizzes 45%, judgment artifacts 30%, studio milestones (CLAUDE.md → tests + Semgrep → deploy + AI usage log) [V] | Summer programme | Jul 21–Aug 13, 2026 [V] | [Assessments](https://ubc-vsp26.github.io/assessments/); [syllabus](https://ubc-vsp26.github.io/syllabus/) | Most explicit "grade judgment" philosophy; stack overlaps ours |
| CMU 15-113/114 *Effective Coding with AI* | Post-intro students [V] | 15-112 [S] | 7 + 7 weeks, ~6 h/week [S] | Free tiers only (Gemini, Kiro, Claude, ChatGPT; VS Code/Cursor) [V] | Portfolio site; deployed full-stack app [V] | Oral "mock interview" evaluations, TA check-ins, prompt logs [V] | University credit | Spring 2026 page | [CMU](https://www.cs.cmu.edu/~113) | Closest audience level; free-tool model; orals |
| UMD CMSC 389A *Modern Software Development with GenAI* | CS students [V] | CMSC216, CMSC250 [V] | Semester | Claude Code Pro ($20/mo, student-paid) [V], FastAPI, Docker [V] | NA | Evaluates AI-generated test suites [V] | Credit | Fall 2026 [V] | [UMD syllabus](https://www.cs.umd.edu/class/fall2026/cmsc389A/Syllabus.html) | Shows paid-subscription requirement in a credit course |
| CRSS-AI *Agentic SE Course* (open curriculum) | Developers | NA | 5 × 1 h live + pre-work [V] | Tool-agnostic | Optional capstone [V] | Reading checks with answer keys [V] | Open | Reviewed Aug 2026; commit 2026-10-01 [V] | [Repo](https://github.com/CRSS-AI/agentic-se-course-early-2026) | Dated currency audit = model for maintenance |
| Maven, *Elite AI Assisted Coding* (Eleanor Berger) | Developers | NA | 6 live sessions, 27 lessons [V] | Copilot, Claude Code, Codex, OpenCode, Cursor [V] | Tiered homework [V] | NA | Price NA | Next cohort "week of June 22" | [Maven](https://maven.com/agentic-ventures/ai-coding) | Vendor-agnostic, tiered homework; 4.6 from 89 reviews |
| DeepLearning.AI × Anthropic, *Claude Code: A Highly Agentic Coding Assistant* | Intermediate [S] | NA | 1 h 50 min [S] | Claude Code, Playwright/Figma MCP [S] | Extend an existing RAG codebase; refactor notebook; Figma → app [S] | 1 graded assignment [S] | NA (403) | NA | [DeepLearning.AI](https://deeplearning.ai/short-courses/claude-code-a-highly-agentic-coding-assistant) | Brownfield-first project design |
| Simon Willison, NICAR 2026 *Coding agents for data analysis* | Data journalists (non-developers) [V] | NA | 3 h workshop [V] | Codespaces, Claude Code, Codex [V] | Data querying, cleaning, scraping [V] | None | Free handout | March 2026 | [Handout](https://simonw.github.io/nicar-2026-coding-agents/) | Only verified offering for non-developers using CLI agents; cloud-setup model |

### Official vendor training (technical coverage, not complete courses)

| Provider / course | Audience | Prerequisites | Duration | Content | Assessment | Price | Update date | Sources | Why selected |
|---|---|---|---|---|---|---|---|---|---|
| Anthropic Academy, *Claude Code 101* | New and experienced developers [V] | Editor and command-line familiarity; paid Claude plan or API key [V] | NA | Install; Explore → Plan → Code → Commit; context management; CLAUDE.md, subagents, skills, MCP, hooks [V] | Quiz, certificate [V] | Free [V] | NA | [Skilljar](https://anthropic.skilljar.com/claude-code-101) | Defines the vendor "core" topic set |
| Anthropic Academy, *Claude Code in Action* | Existing Claude Code users [V] | Same | NA | Now about long unsupervised runs, verification skills, permission modes, hooks, headless/GitHub Actions [V] | Quiz [V] | Free [V] | NA | [Skilljar](https://anthropic.skilljar.com/claude-code-in-action) | Shows how fast vendor course scope shifts |
| OpenAI Academy, *Codex Bootcamp* 101/201/301 | Developers and technical teams [V] | NA | 3 × 1 h live [V] | Scoping, context, steering, review → shared context, approvals, skills, tools → sub-agents, permissions, SDK [V] | Certificate for full attendance [S] | NA | 2026-09-23 to 10-07 [V] | [OpenAI Academy](https://academy.openai.com/public/clubs/builders-etkn1/resources/codex-bootcamp-2026-09-23) | Codex equivalent of the vendor core |
| OpenAI Academy, *Codex for Beginners* | "Including those without technical experience" [V] | None | 1 h livestream, replay [V] | Non-technical use cases, Q&A [V] | None | Free | 2026-04-21 [V] | [Event](https://academy.openai.com/en/public/events/codex-for-beginners-wsz3p1tg0r) | Only vendor item aimed at non-technical users |
| Microsoft Learn / GitHub Skills (Copilot) | Developers | GitHub account | Modules; GitHub Skills exercise "< 1 h" [S] | Agent mode, coding agent, code review, Spaces [V] | Applied Skills assessments [V] | Free | Hub dated 2025-10-23 [V] | [MS Learn hub](https://learn.microsoft.com/en-us/training/topics/ignite/github) | Free-tier fallback path; Codespace-based labs |
| Cursor Learn; Gemini CLI docs | Developers | NA | NA | Fundamentals; Gemini CLI tutorials [V] | NA | Free | NA | [Cursor Learn](https://cursor.com/learn); [Gemini CLI docs](https://geminicli.com/docs/) | Completeness; Gemini CLI free tier ended (see below) |

Three conclusions follow. First, the only beginner offerings near 25–30 hours are ZTM (video, JavaScript, no visible testing module) and Czechitas' own *Vibe coding v praxi* (live, but HTML/CSS/JS on a no-code platform) **[V]**. Second, vendor material is free, short and undated, so it can serve as optional pre-reading but cannot be cited as a stable reference **[I]**. Third, quality evidence is thin everywhere: agent-specific beginner courses have small rating samples (4.2 from 13, 4.5 from 30, 4.9 from 8 reviews), specialization ratings exceed enrolment and evidently aggregate older courses, and no provider publishes completion or outcome data ([Coursera specialization](https://www-cloudfront-alias.coursera.org/specializations/build-anything-with-ai); [Maven](https://maven.com/alpha-clarity/claude-code-for-beginners)). The most trustworthy quality signal is a public, versioned rubric, which only the university courses provide ([Stanford repo](https://github.com/mihail911/modern-software-dev-assignments)).

## Coverage depth, not breadth, separates the strongest offerings

The matrix compares the provisional outline and the revised proposal with the strongest offerings. **M** = mentioned or taught on the syllabus; **P** = a named exercise, assignment or planned hands-on practice; **A** = graded or explicitly checked; **—** = not visible in public materials. For the two Czechitas plans, letters describe *planned* depth; the provisional outline defines no assessment, so it cannot exceed P. Competitor cells reflect only what public syllabi show, so a dash means "not visible", not "absent".

| Topic | Provisional outline | Revised proposal | Vanderbilt Build Apps | Scrimba Claude Code | ZTM | Czechitas v praxi | Stanford CS146S | UBC VSP26 | CMU 15-113 | Claude Code 101 |
|---|---|---|---|---|---|---|---|---|---|---|
| Code literacy / reading unfamiliar code | P (L1–2, L7) | **A** (exit tickets, walkthrough) | — | M | M (HTML/JS) | M (HTML/CSS/JS) | P (OSS repos) | — | A (orals) | — |
| Environment setup, terminal, dependencies | P (L1, L4) | P + A (setup check) | — | M | M | — (platform) | P | — | — | M |
| Requirements / acceptance criteria | M (L5 plan) | **A** | M; builds A | M (plan mode) | M | M | M (spec-driven) | A (design doc, user stories) | P | M |
| Context and task instructions, instruction files | P (L4, L9) | **A** (AGENTS.md in capstone) | M (context folder) | M | M | — | A | A (CLAUDE.md) | — | M |
| Explore → plan → implement on existing repo | P (L5, L7) | P (L4, L8) | — | M | — | — | A | P | M | M |
| Git diff, checkpoints, rollback | P (L3) | **A** | — | M | M | M | M [S] | P | — | M |
| Debugging and recovering from agent failure | P (L2, L6) | **A** (recovery logged) | M (silent failures) | M | — | M | A (forced failure) | — | — | — |
| Unit / integration / end-to-end tests | P (L6, L7) | **A** (unit/integration); P (e2e) | M | M | — | M (user testing) | A | A | — | — |
| Independent verification beyond the agent's tests | P (L6) | **A** (coverage audit, seeded faults) | M | — | — | — | A (observed vs inferred) | A (critique dossier) | A | — |
| Memory, persistent instructions, skills | M/P (L9) | P (skill + trigger test) | — | M | — | — | A | — | — | M |
| MCP and external tools | M (L9) | M (demo) | — | M | M | — | A | A | — | M |
| Sub-agents and parallel work | M (L9) | P (fresh-context reviewer only) | — | M | — | — | A (trace analysis) | — | — | M |
| Permissions, secrets, prompt injection, dependency risk | M (L4) | **A** | M (reading) | M | — | — | A (secret deductions) | A (Semgrep) | — | — |
| Frontend / backend / database concepts | P (Django, FastAPI/React) | P (Django; API + plain frontend) | — | — | P | P | — | A | A | — |
| Deployment, configuration, logs | P (L8) | **A** | M | — | P | P | M [S] | A | A | — |
| Model selection and cost | M (L4) | P | M (sister course) | — | M | — | — | — | — | — |
| When to intervene, restart, simplify, ask a human | — | P + A (log) | — | — | — | — | — | — | — | — |
| Calibration and AI usage / process log (added) | — | **A** | — | — | — | — | A (labelled claims) | A (AI usage log) | A (prompt logs) | — |

Sources: [Vanderbilt](https://www.coursera.org/learn/build-apps-with-ai); [Scrimba](https://www-cloudfront-alias.coursera.org/learn/introduction-to-claude-code); [ZTM](https://zerotomastery.io/courses/learn-vibe-coding/); [Czechitas](https://www.czechitas.cz/kurzy/vibe-coding-v-praxi-vytvor-si-vlastni-web-s-ai-bez-programovani); [CS146S week 1](https://github.com/mihail911/modern-software-dev-assignments/blob/main/week1/assignment.md), [week 2](https://github.com/mihail911/modern-software-dev-assignments/blob/main/week2/assignment.md), [week 3](https://github.com/mihail911/modern-software-dev-assignments/blob/main/week3/assignment.md); [UBC](https://ubc-vsp26.github.io/assessments/); [CMU](https://www.cs.cmu.edu/~113); [Claude Code 101](https://anthropic.skilljar.com/claude-code-101).

The pattern is stark. Among beginner offerings, almost everything sits at "mentioned"; the only assessed items are whole-app builds, AI-graded on Coursera **[V]**. Assessment of judgment (verification evidence, critique of AI output, explaining code orally) appears only in university courses for programmers. The provisional outline already plans more *practice* than any beginner competitor, but without an assessment layer it would look, from the outside, like a longer tool tour. The revised proposal's advantage is the column of A's in the verification, security, Git and explanation rows, not the number of rows.

Several topics are valuable but absent from the brief's list: **calibration** (predicting whether a change works before checking, motivated by METR's finding that experienced developers were 19% slower with AI while believing they were about 20% faster ([Simon Willison summary](https://simonwillison.net/2025/Jul/12/ai-open-source-productivity/))); **dependency existence checks** against hallucinated package names ([CSA research note](https://labs.cloudsecurityalliance.org/research/csa-research-note-slopsquatting-ai-supply-chain-20260419-csa/)); **process or AI usage logs** ([UBC](https://ubc-vsp26.github.io/assessments/); [CMU](https://www.cs.cmu.edu/~113)); **visual and manual verification** (screenshot comparison, scripted user journeys) ([Claude Code best practices](https://code.claude.com/docs/en/best-practices)); and **realistic expectations about agent output**, for which the corpus finding that 45.1% of merged Claude Code PRs in open-source projects still needed human revision is a useful classroom number ([arXiv 2509.14745](https://arxiv.org/pdf/2509.14745)).

## The provisional outline needs reordering more than new content

### Critical evaluation of the provisional outline and the existing web outline

The provisional outline's spine (literacy → Git → agent operation → workflow on Django → testing → unfamiliar repo → deployment → advanced → capstone) mirrors the topic list on which university courses converge **[I]** ([Stanford CS146S](https://themodernsoftware.dev/); [UBC syllabus](https://ubc-vsp26.github.io/syllabus/)), so it is not idiosyncratic. Its problems are ordering and load.

**Two early Python lectures.** The organizer's debugger idea, using breakpoints to make execution flow visible, is pedagogically sound and maps onto PRIMM's *Investigate* step. But spending lectures 1–2 on Python and lecture 3 on Git means the agent's real workflow begins at lecture 5, halfway through the course. The pedagogy notes find no study comparing front-loaded with integrated Python in an agent course; the recommendation to integrate rests on PRIMM, Parsons-problem and subgoal-label evidence ([Raspberry Pi PRIMM slides](https://www.raspberrypi.org/app/uploads/2022/08/Teaching_Programming_with_PRIMM-1.pdf); [Margulieux subgoals](https://www.raspberrypi.org/app/uploads/2020/07/Using-subgoal-labels-to-reduce-cognitive-load-in-introductory-programming.pdf)) and on UCSD's integrated redesign ([arXiv 2406.15379](https://arxiv.org/pdf/2406.15379)). A further argument is that reading *agent* code is harder than reading textbook code because of unfamiliar idioms ([arXiv 2504.19037](https://arxiv.org/pdf/2504.19037)), so literacy practice should happen on the code learners will actually review. The steelman for front-loading is real: weaker learners need more structure, not less, because AI widens the gap between strong and struggling novices ([arXiv 2405.17739](https://arxiv.org/abs/2405.17739v1)). The revised syllabus therefore keeps a structured reading kit across lectures 1–2 but delivers it through agent-generated examples, and adds recurring drills afterwards.

**Git after agent use.** In the provisional order, learners first let an agent edit files in lecture 1 and learn rollback in lecture 3. Because Claude Code's native Windows install has no sandbox and its default starting mode is now auto ([Claude Code setup](https://code.claude.com/docs/en/setup); [Claude Code security](https://code.claude.com/docs/en/security)), Git and an "ask before edit" mode should come first. The delivery notes recommend graduating to auto-edit only after learners can use `git restore` **[I]**.

**Django plus FastAPI/React.** The transfer idea from the brainstorming is excellent: getting an unfamiliar repository running is "super authentic agent usage", and a deliberately broken API contract caught by an end-to-end test but missed by unit tests is a memorable lesson. The cost is a JavaScript toolchain (Node.js, npm, a React build) on Windows laptops, a second language, and a third architecture in a course whose learners are still learning to read Python. The revision keeps the transfer and the broken-contract lesson but uses a small FastAPI service with a pre-built plain HTML/JS page served as static files, so no Node install is needed; a React variant becomes an optional extension or instructor demo. This is design judgment supported only by experience reports that setup is the leading novice barrier ([arXiv 2008.00315](https://arxiv.org/pdf/2008.00315)).

**One lecture for context, memory, instructions, skills, MCP and sub-agents.** That is six vendor-specific concepts in 150 minutes, which reproduces the "feature tour" the market already offers. The revision moves instruction files to lecture 4, where the "we keep repeating ourselves" moment occurs naturally, and keeps hands-on time in lecture 9 for the two practices with the clearest beginner payoff: a skill with a trigger test and a fresh-context reviewer.

**The existing public web outline** ([osnova-python-ai.md](../knowledgebase/osnova-python-ai.md)) differs from the provisional outline in ways that need reconciling. It requires ChatGPT Plus or higher (Codex) with Claude Pro as an alternative, while the course memory lists the agent product and budget as "not yet established". It promises "programovat v Pythonu od úplných základů" and spends three lectures on Python syntax, which conflicts with the memory's goal that writing code from scratch is not central. It builds a greenfield personal project from lecture 6, has no existing-codebase or unfamiliar-repo work, mentions Docker in lecture 9, and treats Skills and MCP as a "taster". Its strengths are worth keeping: product-thinking and Definition of Done before building, a security-and-context lecture, a final audit with "what AI wrote vs what I understand" reflection, and the certificate rule of 80% attendance plus a finished project. The revised syllabus below borrows those strengths.

### Prioritized gap analysis

Each addition names what funds it. Time estimates refer to the 150-minute core unless stated.

| Priority | Addition | Where | Funded by (shortened, replaced or removed) |
|---|---|---|---|
| **Essential** | Acceptance criteria and spec interview before prompting (ChatGPT power users interview themselves into a spec, then the agent plans) ([Harper Reed](https://harper.blog/2025/02/16/my-llm-codegen-workflow-atm/); [Claude Code best practices](https://code.claude.com/docs/en/best-practices)) | L3, every later task | Second Python lecture merged into L1–2 reading kit |
| **Essential** | Criteria-coverage audit and seeded-fault review (tests pass but wrong requirement; hard-coded secret; unrequested file change; nonexistent package) | L5, L6, capstone | FastAPI/React lecture reduced to half-scope transfer lab; debugger reduced from a lecture to a 25-minute segment plus reuse |
| **Essential** | Security thread: `.gitignore`/`.env`, permission modes, prompt-injection demo, dependency-existence check, Django deploy checklist | L1, L4, L6, L7 | MCP and parallel sub-agents moved from hands-on to demo |
| **Essential** | Git checkpoints and "ask" permission mode before autonomous edits | L1–2 | Reordering only; the standalone Git lecture (old L3) disappears |
| **Essential** | Recovery skills: interrupt, rewind, `/clear`-style fresh session, revert, "two failed corrections → restart", when to ask a human ([best practices](https://code.claude.com/docs/en/best-practices)) | L3, L6 | "Models and usage" talk shortened to a 15-minute segment |
| **Essential** | Pre-course setup clinic and checker script | Before L1 (outside the 25–30 h) | Removes ~45 minutes of installation from L1 |
| **Essential** | Process log, exit tickets and capstone walkthrough | Every lecture (5–10 min), L10 | Absorbed from closing segments; capstone presentations replace demo-only showcase |
| **Essential** | Instruction file (AGENTS.md) authored by learners | L4 | Moved from L9 |
| **Valuable if time permits** | Skill authoring with should-fire / near-miss trigger tests ([CS146S week 3](https://github.com/mihail911/modern-software-dev-assignments/blob/main/week3/assignment.md)) | L9 core | Advanced-lecture tour of hooks, plugins and memory internals |
| **Valuable** | Fresh-context reviewer (sub-agent or second session reviewing the diff against the plan) | L9 core | Same |
| **Valuable** | End-to-end check of a user journey (scripted API/HTTP check in core; Playwright browser test in extension) | L8 | React build removed from core |
| **Valuable** | Persistent free Postgres (Neon) via `DATABASE_URL` | L7 extension | Optional 30-minute extension |
| **Valuable** | Same-task comparison of a small vs large model and usage-meter reading | L3 | Shortened theory on model families |
| **Valuable** | Peer review of a classmate's pull request on GitHub | L6 or L10 extension | Extension time |
| **Optional follow-up** | Hooks, plugins, parallel agents and worktrees, cloud/headless agents, GitHub Actions CI, writing an MCP server, Docker, React toolchain, property/mutation testing concepts | Self-study pack or advanced follow-up course | — |
| **Unsuitable** | Proxy-level dissection of an agent session (CS146S week 1), OAuth-scoped MCP server authoring, multi-agent harness engineering, local models (Ollama), Kubernetes or container-based deploys, writing Python from scratch as an assessed skill, vendor plugin-marketplace tours | — | Removed: Docker from the web outline's L9; FastAPI/React as a core build |

## A revised ten-lecture syllabus that fades from demo to independence

The design follows a fading sequence (instructor demo → subgoal-labelled worked example → paired task with a checklist → independent task with only acceptance criteria), which the pedagogy notes derive from worked-example and Parsons evidence but which has not been tested for agents specifically **[I]**. Every lecture contains a predict-run-investigate (PRIMM) moment on agent-generated code and closes with a process-log entry. The capstone is constrained: learners add a self-chosen feature set to the course's Django application or start from a provided minimal Django template, which keeps deployment uniform and makes walkthroughs comparable. Each lecture has a 150-minute core (including a 10-minute break) and an optional 30-minute extension for faster learners or a longer session. Tool commands live in a per-tool appendix, not in lecture text.

**Lecture 0 (pre-course, not counted): setup clinic.** A 60–90-minute online clinic plus a written guide and checker script verify Git for Windows, VS Code, uv (which installs Python), the chosen agent, a GitHub account and the agent subscription. Learners who cannot finish get a GitHub Codespaces fallback.

### Lecture 1 – From chat to agent, safely

| Element | Content |
|---|---|
| Learning outcomes | Explain how a coding agent differs from chat (it reads files, runs commands, edits); open a project folder in VS Code and run a Python script from PowerShell/terminal; run an agent in read-only/ask mode and approve or reject a proposed edit; make a first Git commit as a save point |
| Prerequisites | Setup clinic completed; accounts active |
| Key topics | Folders, paths and the terminal prompt; running `uv run python`; variables, strings, lists and `if` via reading; permission modes as a safety dial; `.gitignore` before the first commit; Git as save points (VS Code Source Control UI) |
| Practical exercise | Agent explains a 30-line provided script; learner predicts output for two inputs, runs it, compares; asks agent for one small change in ask mode, reviews the diff, commits |
| Observable evidence | Exit ticket: predict the output of a 6-line snippet; screenshot of first commit; first process-log entry (what I asked, what the agent did, what I checked) |
| Timing (150) | 15 intro and safety framing · 25 terminal and VS Code tour · 30 PRIMM on the script with agent explanations · 10 break · 30 first agent edit in ask mode · 20 first commit and `.gitignore` · 10 exit ticket and log · 10 buffer for setup issues |
| Extension (30) | Same task with a second agent or the desktop app; compare permission prompts |

### Lecture 2 – Reading code and undoing mistakes

| Element | Content |
|---|---|
| Learning outcomes | Trace loops, functions and exceptions with the debugger; read a traceback and locate the failing line; inspect a diff, restore a file and return to an earlier commit; push to GitHub |
| Prerequisites | L1 |
| Key topics | `for`, functions, parameters and return values, `try/except`; debugger breakpoints as a "slow-motion" view of execution; Parsons-style reordering of agent code; `git diff`, `git restore`, `git log`; remote repository |
| Practical exercise | Agent writes a function with a deliberately ambiguous spec; learner steps through it in the debugger, triggers an exception, then lets the agent "improve" the code, rejects one hunk and restores it with Git |
| Observable evidence | Learner can point to where execution jumps on exception; repository on GitHub with at least one reverted change visible in history |
| Timing (150) | 10 recap check · 25 reading kit (loops, functions) via agent-explained examples · 25 debugger walkthrough · 10 break · 15 tracebacks · 35 diff, restore, revert exercise · 15 push to GitHub · 10 exit ticket and log · 5 buffer |
| Extension (30) | Parsons puzzle set on agent-generated functions; "explain in plain English" challenge |

### Lecture 3 – Specify before you prompt

| Element | Content |
|---|---|
| Learning outcomes | Turn a vague idea into a short spec with acceptance criteria; run explore → plan → implement → verify → commit on a small greenfield Python tool; recognise when to interrupt, rewind or restart a session; read the usage meter and choose a lighter model for routine work |
| Prerequisites | L2 |
| Key topics | Spec interview (ChatGPT or agent asks questions one at a time); inputs, outputs, edge cases, out-of-scope; plan mode / read-only planning; context window as a limited resource; correcting early vs restarting fresh; model and cost trade-offs without hard-coded model names |
| Practical exercise | Build a small CLI data tool (e.g. CSV summary) from the learner's own spec; deliberately vague first prompt vs spec-driven prompt, compare outcomes |
| Observable evidence | Spec with at least five testable acceptance criteria; process log noting one plan change the learner requested |
| Timing (150) | 10 check · 20 why specs ("substance beats style" ([arXiv 2410.19792](https://arxiv.org/html/2410.19792v1))) · 25 spec interview · 25 plan review and edit · 10 break · 35 implement and verify against criteria · 15 recovery drill (interrupt, rewind, restart) · 10 log |
| Extension (30) | Same task on a smaller and a larger model; compare quality, speed and usage |

### Lecture 4 – Working inside an existing Django application

| Element | Content |
|---|---|
| Learning outcomes | Describe a request's path through URL → view → template → model → database; ask the agent to map an unfamiliar repo before changing it; write an AGENTS.md with run/test commands and constraints; add a small feature with a migration and run it locally |
| Prerequisites | L3 |
| Key topics | Django project anatomy, SQLite locally, migrations; repository exploration questions; instruction files (one AGENTS.md works for Codex and, when no CLAUDE.md exists, Claude Code ([memory docs](https://code.claude.com/docs/en/memory); [agents.md](https://agents.md/))); approving install commands only after the agent explains them |
| Practical exercise | Provided small Django app (e.g. a reading-list or event-signup app); learner gets it running, writes AGENTS.md, then adds a field plus form change via plan → implement |
| Observable evidence | Learner's annotated map of where the feature lives; AGENTS.md committed; feature works on localhost |
| Timing (150) | 10 check · 25 Django mental model with a debugger trace of one request · 25 agent-led repo exploration · 15 write AGENTS.md · 10 break · 50 feature via plan → implement → run · 10 commit and log · 5 buffer |
| Extension (30) | Fresh session with and without AGENTS.md; compare how much re-explaining was needed |

### Lecture 5 – Tests are evidence, not proof

| Element | Content |
|---|---|
| Learning outcomes | Run unit and integration tests and read failures; write acceptance criteria before the agent writes tests; audit which criteria the agent's tests actually cover; detect a test suite that passes while the requirement is wrong |
| Prerequisites | L4 |
| Key topics | Django test client, pytest basics; red/green: a failing test that reproduces a bug, then the fix ([best practices](https://code.claude.com/docs/en/best-practices)); "first run the tests"; criteria-coverage table; manual user-journey check |
| Practical exercise | Agent implements a feature and its tests; a seeded requirement misreading leaves all tests green; learners find which criterion is unverified, add the missing test, watch it fail, then fix |
| Observable evidence | **Checkpoint review 1**: criteria-coverage table submitted with one missing case identified and tested |
| Timing (150) | 10 check · 20 what tests prove and don't · 20 run and read failures · 10 break · 45 seeded-fault coverage audit · 30 red/green bug fix · 15 log and debrief |
| Extension (30) | Ask a fresh session to write tests from criteria only, then compare with the original agent's tests |

### Lecture 6 – Reviewing agent work: security, injection and recovery

| Element | Content |
|---|---|
| Learning outcomes | Review an agent-produced change against a checklist; find a hard-coded secret, an unrequested change and a nonexistent or suspicious dependency; explain how instructions hidden in a README or web page can hijack an agent; recover a broken session with Git and a fresh start |
| Prerequisites | L5 |
| Key topics | Review checklist (scope, secrets, dependencies, auth/permissions, tests run, diff read); `.env` and environment variables; GitHub push protection covers only public repos ([GitHub docs](https://docs.github.com/en/code-security/secret-scanning/introduction/about-push-protection)); prompt injection ([Codex security](https://learn.chatgpt.com/docs/agent-approvals-security)); never use full-access or bypass modes; verifying a package on PyPI |
| Practical exercise | Seeded-fault pull request on the course Django app with four planted defects; learners review it on GitHub, write a verdict, and request or make fixes; instructor demo of a prompt-injection README |
| Observable evidence | **Checkpoint review 2**: written review verdict listing found defects with evidence; number of planted defects found is recorded (not graded harshly, used as calibration) |
| Timing (150) | 10 check · 20 why AI code is often insecure and why users are overconfident · 15 injection demo · 10 break · 50 seeded PR review · 25 fix and re-verify · 10 recovery drill · 10 log |
| Extension (30) | Peer review of a classmate's feature branch; run the agent's built-in security review and compare with the human findings |

### Lecture 7 – Ship it: deploying Django on a free service

| Element | Content |
|---|---|
| Learning outcomes | Deploy the Django app from GitHub to a free host; configure `SECRET_KEY`, `DEBUG`, `ALLOWED_HOSTS` and database settings through environment variables; read platform logs to diagnose a failed deploy; explain why SQLite on an ephemeral disk loses data |
| Prerequisites | L6; host account |
| Key topics | Render Free (sleep after 15 minutes, ephemeral disk, free Postgres expires after 30 days ([Render](https://render.com/docs/free))); Render's Django guide (build script, gunicorn, WhiteNoise) ([Render Django](https://render.com/docs/deploy-django)); Django `check --deploy` ([Django checklist](https://docs.djangoproject.com/en/stable/howto/deployment/checklist/)); PythonAnywhere as persistent-SQLite fallback ([pricing](https://www.pythonanywhere.com/pricing/)) |
| Practical exercise | Agent proposes a deployment plan which the learner reviews; first deploy intentionally fails (`DEBUG=False` without `ALLOWED_HOSTS`); learner reads logs, fixes with the agent, redeploys |
| Observable evidence | Public URL works; log excerpt and fix recorded in process log; no secret in repository |
| Timing (150) | 10 check · 20 what deployment means (environments, config, logs) · 15 platform walkthrough · 10 break · 50 deploy with planned failure · 25 fix and redeploy · 10 `check --deploy` · 10 log |
| Extension (30) | Connect free Neon Postgres via `DATABASE_URL` so data survives redeploys ([Neon pricing](https://neon.com/pricing)) |

### Lecture 8 – Transfer: an unfamiliar repository and an end-to-end check

| Element | Content |
|---|---|
| Learning outcomes | Get an unfamiliar repo running with the agent from its README; explain how an API backend and a separate frontend differ from Django's server-rendered pages; find a bug that unit tests miss but a user-journey check catches; draft the capstone spec |
| Prerequisites | L7 |
| Key topics | Reading a README and dependency file; OS-specific commands (Windows vs macOS shown side by side); HTTP, JSON, API contract; scripted end-to-end check; capstone scoping and Definition of Done |
| Practical exercise | Small FastAPI service with a pre-built plain HTML/JS page; seeded contract mismatch (field renamed in API, page still reads old name) passes unit tests; learners reproduce via browser, add an end-to-end check, fix |
| Observable evidence | Running app; failing-then-passing end-to-end check committed; capstone spec draft with acceptance criteria |
| Timing (150) | 10 check · 15 architecture contrast · 35 get it running with the agent · 10 break · 40 contract bug and end-to-end check · 30 capstone spec interview · 10 log |
| Extension (30) | React version of the same frontend as instructor-led demo, or a Playwright browser test |

### Lecture 9 – Reusable agent know-how and capstone sprint 1

| Element | Content |
|---|---|
| Learning outcomes | Manage context deliberately (fresh session per task, compacting, scoped instructions); author a small skill and test that it fires on intended prompts and not on a near miss; use a fresh-context reviewer on one's own diff; explain what MCP adds and why only trusted servers should be connected |
| Prerequisites | L8; capstone spec approved |
| Key topics | Agent Skills open standard ([agentskills.io](https://agentskills.io/)); "run it manually once first"; reviewer sub-agent or second session; MCP demonstration (e.g. browser or GitHub server) and trust ([Claude Code security](https://code.claude.com/docs/en/security)); hooks and parallel agents named as follow-up only |
| Practical exercise | Write a "review my diff against the spec" skill, test with three should-fire prompts and one near miss; then capstone sprint with the skill and a fresh-context review |
| Observable evidence | Skill file plus trigger-test notes committed; reviewer output with the learner's accept/reject decision for each finding |
| Timing (150) | 10 check · 15 context management · 35 skill authoring and trigger tests · 15 MCP demo · 10 break · 55 capstone sprint · 10 log |
| Extension (30) | Instructor demo of parallel sub-agents or worktrees; discussion of cost implications |

### Lecture 10 – Capstone lab, audit and walkthrough

| Element | Content |
|---|---|
| Learning outcomes | Finish, verify and redeploy the capstone; audit it with the review checklist; explain one function, one test and one overridden agent decision in a five-minute walkthrough; reflect on what the agent wrote vs what the learner understands |
| Prerequisites | Capstone homework between L9 and L10 |
| Key topics | Final verification against acceptance criteria; README and AGENTS.md as handover; retrospective |
| Practical exercise | Lab time with mentor rounds, then walkthroughs in small groups |
| Observable evidence | Capstone rubric scored; deployed URL; final process log |
| Timing (150) | 10 plan · 60 lab with mentor check-ins · 10 break · 55 walkthroughs (groups of 5–6 per mentor, ~5 min each plus feedback) · 15 retrospective and next steps |
| Extension (30) | Public showcase or recorded demo for learners' portfolios |

The capstone is a stretch in a 25–30-hour course, so homework matters: the spec is drafted at the end of L8 and the build is mostly done between L9 and L10. If homework expectations end up low, the capstone should shrink to one feature on the course app rather than an own project.

## Assessment should score judgment the agent cannot supply

### Lightweight progress checks

Every lecture opens with a two-to-three-question **recap check** done without the agent (predict an output, spot a bug in five lines, name the right Git command), borrowing UBC's no-AI quiz idea at much lower stakes ([UBC](https://ubc-vsp26.github.io/assessments/)). Every lecture closes with a **process-log entry** of five fields: what I asked, what the agent did, what I checked and how, what I rejected or changed and why, and my prediction vs the actual result. The log operationalises calibration and doubles as the AI usage log that UBC and CMU require ([CMU](https://www.cs.cmu.edu/~113)). Two **checkpoint reviews** (L5 coverage audit, L6 seeded-PR review) give each learner written feedback before the capstone; the planted-defect count found in L6 can be repeated in L10 on a fresh seeded PR to show growth, which is the course's best before/after evidence. Mentors can run **"explain this diff" micro-orals** of two minutes during lab rounds, the cheap version of CMU's mock-interview evaluations **[I]**.

### Capstone rubric

The rubric scores judgment and the resulting application, not feature count. Weights total 100; a certificate could require Competent or better on criteria 2 and 7 in addition to the 80% attendance rule already used by Czechitas.

| # | Criterion | Weight | Beginning (1) | Developing (2) | Competent (3) | Strong (4) |
|---|---|---|---|---|---|---|
| 1 | Specification | 15 | Vague goal, no criteria | Criteria listed but untestable | Testable criteria incl. one edge case and out-of-scope | Criteria refined during work, changes logged with reasons |
| 2 | Verification evidence | 25 | Relies on agent's claim | Ran agent's tests only | Criteria-coverage table; tests run by learner; manual journey checked on deployed URL | Found and closed a coverage gap; added a test that failed first |
| 3 | Judgment about agent output | 20 | Accepted everything | Rejected changes without stating why | At least two documented rejections or corrections with reasons | Caught a substantive defect (logic, security, scope) and explained its impact |
| 4 | Git and change hygiene | 10 | One large commit | Several commits, unclear messages | Small commits with clear messages; diff reviewed before each | Used revert/restore to recover from a bad agent change, documented |
| 5 | Security and configuration | 10 | Secret in repo or `DEBUG=True` in production | Secrets externalised but no checklist | `.env` ignored, env vars on host, `check --deploy` run, dependencies verified | Also identified and mitigated an injection or permission risk |
| 6 | Working, deployed application | 10 | Not running | Runs locally only | Deployed; meets core criteria | Deployed; handles errors gracefully; README lets a stranger run it |
| 7 | Explanation (walkthrough) | 10 | Cannot explain the code | Explains with heavy prompting | Explains one function, one test and one decision clearly | Explains trade-offs and what they would do differently |

This design adapts UBC's milestone checklist (instruction file → tests plus security scan → deploy plus usage log) and CMU's "can't explain it, can't submit it" rule to a non-credit course ([UBC](https://ubc-vsp26.github.io/assessments/); [CMU](https://www.cs.cmu.edu/~113)). No validated rubric for agentic-coding judgment exists, so the criteria are design judgment and should be calibrated after the first cohort by double-scoring a sample of walkthroughs.

## Five differentiators the course can prove, not just claim

**Verification-first teaching with seeded faults.** No beginner offering visibly uses planted defects or deliberately flawed agent output; Vanderbilt's "Silent Failure Audit" is the nearest idea and is ungraded ([Coursera](https://www.coursera.org/learn/build-apps-with-ai)). The course can demonstrate this advantage by publishing an anonymised before/after statistic: the share of planted defects learners found in L6 versus a fresh seeded PR in L10.

**Real codebases and a genuine transfer task.** Nearly all beginner projects are greenfield; brownfield work appears only as single lessons ([Scrimba](https://www-cloudfront-alias.coursera.org/learn/introduction-to-claude-code); [Vibe Code School](https://vibecodeschool.com/courses/claude-code-vibe-coding)). The evidence is each learner's commit history on two unfamiliar repositories and a working end-to-end check.

**Python reading literacy for non-programmers.** None of the agent courses teaches code reading in Python; where literacy appears, it is HTML/CSS/JS ([ZTM](https://zerotomastery.io/courses/learn-vibe-coding/); [Czechitas v praxi](https://www.czechitas.cz/kurzy/vibe-coding-v-praxi-vytvor-si-vlastni-web-s-ai-bez-programovani)). This also differentiates the course clearly from Czechitas' own web-focused offering. Demonstration: recap-check scores across lectures and recorded walkthroughs in which learners explain their own code.

**Judgment assessed by humans rather than AI-graded output.** Coursera's beginner assignments are AI-graded builds; UBC- and CMU-style judgment assessment exists only for programmers **[V/I]**. Publishing the rubric and a sample annotated walkthrough lets prospective learners and employers see what was assessed.

**Windows-first, tool-agnostic, dated materials with live support.** No landing page of any beginner competitor addresses Windows/PowerShell **[I]**. The course can show a "verified on date X with version Y" stamp per lecture, a per-tool appendix for Codex and Claude Code, and a reported setup success rate from the pre-course clinic.

## Delivery depends on one budget decision and a refresh routine

### Operating systems and setup

Both Codex and Claude Code now run natively on Windows from PowerShell, and WSL is optional for both ([Claude Code setup](https://code.claude.com/docs/en/setup); [Codex Windows](https://learn.chatgpt.com/docs/windows/windows-sandbox)). The important asymmetry is sandboxing: Codex ships a native Windows sandbox whose preferred "elevated" mode needs administrator-approved setup, which can fail on locked-down work laptops, while Claude Code's sandbox is unsupported on native Windows and requires WSL2, so Windows learners rely on permission modes. On Windows, Python installation changed: the classic full installer is deprecated since 3.14, and the Python Install Manager is recommended ([Python on Windows](https://docs.python.org/3/using/windows.html)). The notes recommend uv, which downloads Python itself and sidesteps the PowerShell execution-policy error on `Activate.ps1` ([uv](https://docs.astral.sh/uv/guides/install-python/); [venv docs](https://docs.python.org/3/library/venv.html)). The recommended stack is Git for Windows, VS Code, uv and the agent's native installer, with Node.js needed only for the optional React extension. Known beginner failure modes to cover in the setup guide are the Microsoft Store `python` alias stub, PATH not refreshed until a new terminal, PowerShell vs CMD confusion, antivirus blocking `irm | iex`, old Windows 10 builds and (an unverified risk) OneDrive-synced project folders **[I]**. macOS and Linux follow the same steps with shell-script installers; materials should show Windows commands first and macOS/Linux variants alongside.

GitHub Codespaces is a fallback for broken laptops, but desktop-app agents do not run there, and the free allowance is ambiguous: the fetched billing page shows "120 hrs" per month on personal accounts, while historical documentation stated 120 *core* hours, which equals 60 hours on the default two-core machine ([GitHub Codespaces billing](https://docs.github.com/en/billing/concepts/product-billing/github-codespaces)). **This conflict is unresolved**; re-check before relying on Codespaces for whole lectures.

### Learner costs and conflicting price data

Deployment can be free: Render Free deploys from GitHub without a stated card requirement, Neon Free Postgres is permanent without a card, and PythonAnywhere Free keeps SQLite persistent but now requires monthly renewal for new users and has no Git auto-deploy ([Render](https://render.com/docs/free); [Neon](https://neon.com/pricing); [PythonAnywhere blog](https://blog.pythonanywhere.com/221/)). Fly.io, Koyeb, Cloud Run and Heroku require a card, Hugging Face Docker Spaces now require a paid plan, and Railway's no-card trial lasts only 30 days, so all are unsuitable under the no-charge rule ([Fly.io](https://docs.fly.io/about/pricing); [Koyeb](https://www.koyeb.com/docs/faqs/pricing); [HF Spaces](https://huggingface.co/docs/hub/spaces-overview); [Railway](https://railway.com/pricing)). Whether Render requires a card at signup was not verified.

The agent subscription is the real cost, and the notes disagree on several facts. These conflicts are flagged rather than resolved:

| Item | Version A | Version B | Assessment |
|---|---|---|---|
| Claude Pro monthly price | $25 billed monthly, $17/month annual — vendor_training notes, quoting [claude.com/pricing](https://claude.com/pricing) [V] | $20 monthly, $17 annual — delivery notes, same URL [V] | Same page, same day, different readings. Both agree on $17 annual. The $25 figure is quoted verbatim and may be a recent price change; **re-check manually before publishing any figure** |
| Claude Max 20x | "Max starts at $100/month (5x or 20x)" — vendor notes [V] | Summarizer returned $100 for both tiers; historically 20x was $200 — delivery notes flag it unverified | Unresolved; likely a "from $100" rendering artifact. Irrelevant to beginners, who should not need Max |
| Gemini CLI free tier | Unpaid tier and Google One users moved to Antigravity CLI on 2026-06-18 ([geminicli.com/docs](https://geminicli.com/docs/)) [V], corroborated by press ([The Register](https://www.theregister.com/ai-ml/2026/05/20/bye-bye-gemini-cli-google-nudges-devs-toward-antigravity/5243605)) [S] | 1,000 requests/day free with personal Google login ([GitHub README](https://github.com/google-gemini/gemini-cli)) [V] | The official docs statement is more specific and corroborated; the README figure is probably stale. **Treat free Gemini CLI as unavailable** for planning |
| Codex on ChatGPT Free/Go | "Included in every ChatGPT plan, including Free and Go" — vendor notes ([Codex pricing](https://learn.chatgpt.com/docs/pricing)) | Free/Go get Codex only in the desktop app, "subject to rollout", with no published limits — delivery notes, same page | Compatible: Codex is nominally included but restricted and not dependable for a cohort. Plus is the lowest dependable OpenAI tier |
| Codespaces free compute | 120 hrs/month | 120 core hours (= 60 h on 2-core) | Unresolved (see above) |

Given these facts, the defensible baseline is one consumer subscription that includes a coding agent (ChatGPT Plus for Codex or Claude Pro for Claude Code) for the course's duration. Many target learners may already pay for ChatGPT Plus, which is an inference rather than a verified enrolment fact. Copilot Free offers "limited chat and agent usage" and can serve as an emergency fallback, but expect throttling ([Copilot plans](https://github.com/features/copilot/plans)). Czech VAT-inclusive prices were not verified for any vendor, and the total depends on whether lectures run weekly (about 2.5 months) or compressed like *Vibe coding v praxi* (two weeks), which is still undecided. Usage limits are published only as wide ranges (Codex Plus) or not at all (Claude Pro), so heavy in-class use could exhaust a five-hour window; lab tasks should be sized small and learners taught to switch to lighter models **[I]**. **Prices and model names should appear only in a dated "costs and tools" appendix, never in lecture text**; model names in the notes (e.g. Codex's GPT-6.x tiers) already changed several times in the five weeks before the research date ([Codex What's new](https://learn.chatgpt.com/docs/whats-new.md)).

### Maintenance cadence

Claude Code shipped eight releases (2.1.285 to 2.1.292) between 29 September and 6 October 2026, Codex publishes a weekly digest, the Codex documentation moved domains with some deep links now returning 404, and Gemini CLI's free tier disappeared within the last four months ([Claude Code changelog](https://code.claude.com/docs/en/changelog); [learn.chatgpt.com llms.txt](https://learn.chatgpt.com/llms.txt)). The CRSS-AI curriculum's dated audit (link health, publication dates, whether each documented feature is enabled by default) is a ready-made procedure to copy ([CRSS-AI audit note](https://github.com/CRSS-AI/agentic-se-course-early-2026/blob/main/notes/curriculum-refresh-aug-2026.md)).

| Volatility | Materials | Refresh |
|---|---|---|
| High | Agent install commands, permission-mode names and defaults, slash commands, screenshots, plan prices and limits, model names, vendor doc URLs, free-tier conditions of hosts | Before every cohort and on any default change; pin Claude Code to its "stable" channel during a cohort ([setup](https://code.claude.com/docs/en/setup)); record tested versions in each lecture |
| Medium | Python/uv/Django versions, Render and PythonAnywhere deploy steps, Windows setup guide, seeded-fault repos (re-test that faults still survive the current agent) | Each cohort |
| Low | Spec and acceptance-criteria method, explore → plan → implement → verify → commit loop, Git concepts, review and security checklists, rubric, PRIMM drills | Yearly or after rubric calibration |

Seeded-fault exercises need special care: a newer agent may notice and fix the planted defect unprompted, which silently removes the exercise's point. Freeze the seeded repositories as provided code rather than asking the agent to generate the faulty version live.

## Open decisions and the limits of this evidence

### Decisions the organizer must make

The most urgent is the **primary agent and budget**. The public web outline already states that learners need ChatGPT Plus or higher and that Claude Pro is an acceptable alternative, the repository's placeholder title names "Codex CLI a Claude Code", and the course memory records the product and budget as undecided. Either the memory should be updated to record ChatGPT Plus (Codex) as the requirement, or the web page should be changed before enrolment opens. My design judgment favours Codex via ChatGPT Plus as the primary demo tool (many learners likely already pay for it, it has a native Windows sandbox, and AGENTS.md is native) with Claude Code as a supported alternative, but this depends on the elevated sandbox working on learners' laptops and on instructor preference. The remaining open decisions are: session length within 2.5–3 hours and cadence (weekly vs compressed, which changes subscription cost and homework feasibility); delivery mode (online vs in person, which changes setup support); homework expectations, on which the capstone's scope depends; capstone format (feature on the course app vs own small Django app); deployment provider (Render + Neon primary, PythonAnywhere fallback is recommended but not confirmed); cohort size and mentor ratio, which determines whether five-minute walkthroughs are feasible; teaching language; and whether to rename the course, since the web title promises programming "from the basics" rather than directing and evaluating agents.

### What is research-backed and what is design judgment

| Research-backed (with stated strength) | Curriculum-design judgment |
|---|---|
| Novices over-trust AI code and overestimate understanding (qualitative + controlled studies; moderate) | Exact lecture order and minute allocations |
| Delegating code generation lowers learning compared with conceptual use (RCTs, other populations; moderate) | Merging two Python lectures into a reading kit |
| Read-before-write scaffolds (PRIMM, Parsons, subgoals) help novices (quasi-experimental + controlled; moderate, pre-AI) | Choosing FastAPI + plain frontend over React |
| Non-developers verify least systematically (survey; weak) | Which advanced topics are hands-on vs demo |
| Setup is a leading novice barrier (experience reports; weak) | The seeded-fault exercises and their defect mix |
| Vendors converge on explore → plan → implement → verify → commit and on giving the agent a way to verify (vendor docs [V]) | Rubric criteria and weights |
| Free hosting conditions and Windows support (vendor pages [V], with flagged conflicts) | Codex vs Claude Code as primary tool |
| Competitor coverage at "mentioned" level (public syllabi [V]) | Claim that the five differentiators are unique (absence in public syllabi is not proof of absence) |

### Evidence limitations

All competitor lessons, exercises and rubrics are paywalled or locked; DeepLearning.AI pages returned HTTP 403, so its details come from search snippets; and the research notes were extracted with an automated page fetcher, so exact figures should be spot-checked before external use. No provider publishes completion or outcome data, and ratings for agent-specific beginner courses rest on 8–30 reviews. Almost all pedagogy evidence concerns university CS1 students, K-12 learners or professional developers using chat or autocomplete tools, not adult non-programmers directing autonomous agents; no RCT of that population exists. Several cited studies (METR, Pearce et al., Perry et al., the 2019 PRIMM study, CodeAid) were noted from prior knowledge without re-fetching their URLs, and the Fawzy et al. survey is cited through a secondary summary. The adjacent-course search did not reach MIT, Berkeley, TU Delft, Frontend Masters or Pluralsight, and Codex-, Cursor- and Copilot-specific short courses were not researched. The Czechitas *Vibe coding v praxi* run dates may be from a past year.

## Conclusion

The competitive gap is not where the market's marketing points. Beginner courses compete on tool lists and finished apps, while the university courses that grade judgment are closed to non-programmers; the uncontested position is a beginner course that can show, with artefacts, that its graduates catch what agents get wrong. That reframes the provisional outline: its topics are already sufficient, and the remaining work is to front-load safety (Git, ask modes), move the real agent workflow to lecture 3–4, and spend the hours freed from syntax lectures, the React toolchain and the advanced-features tour on seeded faults, coverage audits and walkthroughs.

The design is also fragile in ways a topic list hides. The two largest risks are operational, not pedagogical: an unresolved subscription requirement that the public web page has already decided, and tooling that changes faster than a ten-lecture cohort runs. A dated per-tool appendix, a pre-cohort audit and frozen seeded-fault repositories cost little and protect the course's main differentiator, which only works if the planted mistakes are still there when learners go looking for them.
