# Beginner / non-programmer courses on building software with AI coding agents (benchmark, research date 2026-10-07)

Method note: Evidence comes from public landing pages and syllabus pages, fetched on 2026-10-07. Labels: **[V]** means seen on the primary source page. **[I]** means inferred. **[NA]** means not publicly available or not found. Everything was extracted with an automated page fetcher, so before citing exact numbers externally, spot-check them. Lesson content is paywalled or locked in every case, so this file judges no course's teaching quality. Coverage below is classified only as "mentioned on syllabus" unless a named exercise or assignment is visible. The DeepLearning.AI pages returned HTTP 403 to the fetcher, so details for that course come from search snippets only.

## Which competitor offerings target beginners/non-programmers, and what are their basic parameters?

### Takeaway
About ten relevant offerings exist. Most are short (1–9 h) self-paced video courses or one-shot live workshops. Only three come near the Czechitas course's 25–30 h. ZTM's bootcamp (18 h of video) is the only one with a long syllabus that includes terminal/Git setup. Engeto's academy (250+ h) is a full-stack course with AI tooling, not agent-first. Stanford's live course is short (7.5 h). No beginner offering found combines Python code reading, Git, testing, an existing-codebase workflow and deployment in a live cohort the way the Czechitas plan does.

### Cited Findings

**1. Vanderbilt / Jules White: "Build Apps with AI — From Idea to Working Product" (Coursera)**
- [V] Beginner, 6 h, 5 modules, self-paced, 2 AI-graded assignments ("Your First Web Application", "Build a Web App for Your Own Workflow"). Tools: Claude Code, Claude Cowork, "MAJK", ChatGPT, with "Python or JavaScript" as the essential-tools reading. — [Coursera](https://www.coursera.org/learn/build-apps-with-ai)
- [V] It has a dedicated module, "Testing & Evaluating What You Build". Topics: "Building Trust in Your AI PhD's Work", "Testing Your Build with Real Data", "The Silent Failure Audit", "Getting Your AI PhD to Check Its Own Work", "From User Journeys to Automated Tests — A Non-Technical Guide", and "Visual Testing". This module has no graded assignment. — [Coursera](https://www.coursera.org/learn/build-apps-with-ai)
- [V] Requirements technique: "Specify Requirements with Before and After", "Show AI What You Want — Build a Context Folder", "Best of N Pattern", "Design First". — [Coursera](https://www.coursera.org/learn/build-apps-with-ai)
- [V] Security and maintenance appear only as final readings: "Why Security and Safety Escalate the Moment You Go Public" and "Why Maintenance Gets Harder Over Time". The syllabus has no Git and no terminal. — [Coursera](https://www.coursera.org/learn/build-apps-with-ai)
- [V] Free enrollment is possible; the certificate is paid or via Coursera Plus. No ratings were shown. — [Coursera](https://www.coursera.org/learn/build-apps-with-ai)

**2. Vanderbilt / Jules White: "Build Anything with AI — No Code Required" (Coursera)**
- [V] Beginner, 9 h, 6 modules, 6 AI-graded assignments (dashboard, map/reduce, gap analysis, briefing, etc.). Rated 4.2/5 from 13 reviews, with 6,072 enrolled. Prerequisite wording: "no prior coding required". — [Coursera](https://www-cloudfront-alias.coursera.org/learn/build-anything-with-ai)
- [V] The framework is called "CODER" (Compute, Organize, Display, Reason). The emphasis is on data/file automation and analysis more than app engineering. — [Coursera](https://www-cloudfront-alias.coursera.org/learn/build-anything-with-ai)
- [V] Both courses are bundled in two specializations. "Build Anything with AI: No Code Required" has 4 courses (~40 h) and states the prerequisite as "Basic computer skills, understand files and folders, and have basic experience with a tool like ChatGPT, Claude, or Gemini". "AI Builder" has 6 courses and adds Trustworthy GenAI and GenAI Cybersecurity for Leaders. — [Coursera spec](https://www-cloudfront-alias.coursera.org/specializations/build-anything-with-ai); [Coursera AI Builder](https://www.coursera.org/specializations/ai-builder)
- [V] The specialization pages show 4.8/5 from 8,243 and 9,618 reviews, but only 3,490 and 1,754 enrolled. The review counts are evidently aggregated from older bundled courses such as Prompt Engineering for ChatGPT. — [Coursera spec](https://www-cloudfront-alias.coursera.org/specializations/build-anything-with-ai); [AI Builder](https://www.coursera.org/specializations/ai-builder)
- [V] For contrast, the same instructor's "Claude Code: Software Engineering with Generative AI Agents" is labelled Beginner. However, it requires "Basic software development experience and familiarity with version control (Git)" and "a paid subscription that includes Claude Code". It runs 5 h and covers CLAUDE.md, commands, Git worktrees, subagents and "Ensuring Claude Code Checks Its Own Work". Rated 4.7 from 180 reviews. It is not actually for non-programmers. — [Coursera](https://www.coursera.org/learn/claude-code)

**3. Scrimba: "Vibe Coding Essentials — Build Apps with AI" specialization (Coursera)**
- [V] 5 courses: Vibe Coding with Cursor AI (1 h), with GitHub Copilot (2 h), with Claude Code (3 h), Intro to MCP (1 h), and Learn to code with AI (8 h). Stated audience: beginners with no coding experience (marketers, designers, accountants). Rated 4.4 from 415 reviews, with 22,397 enrolled. Projects: portfolio site, games, Chrome extensions, database apps, deployment via GitHub and Netlify. — [Coursera](https://www.coursera.org/specializations/vibe-coding)
- [V] The component course "Vibe Coding with Claude Code" (instructor Maham Codes) is labelled **Intermediate** despite the beginner specialization. It is 3 h with 25 videos and 2 assignments. Module 1 covers setup, rules and Plan Mode, "Checkpoints and Security Checks", hooks, slash commands, agents, a calendar-app build, and MCP. Module 2 covers context-window management, Skills and plugins, "Exploring a Codebase", "Bugs, Refactoring, and Tests", PRs and docs, and resuming sessions and Git worktrees. Rated 4.5 from 30 reviews, with 10,549 enrolled. — [Coursera](https://www-cloudfront-alias.coursera.org/learn/introduction-to-claude-code)

**4. Zero To Mastery: "The Vibe Coding Bootcamp"**
- [V] 18 h of video, 158+ lessons, 10+ projects, instructor Jacinto Wong. Page says last updated October 2026. The audience spans complete beginners to experienced developers. — [ZTM](https://zerotomastery.io/courses/learn-vibe-coding/)
- [V] The 10 modules include a "Developer Setup" module (terminal, Node.js, Git, GitHub, VS Code). Other modules cover "Becoming a Director", AI editors (Copilot, Cursor, Zed), MCP, local models (Ollama), and a capstone portfolio site with interview prep. Projects are all JavaScript/web (games, a news reader with a proxy server, a PWA recipe app, Next.js). — [ZTM](https://zerotomastery.io/courses/learn-vibe-coding/)
- [V] Pricing: $299 for the single course, $25/month, $299/year, or $1,299 lifetime. — [ZTM](https://zerotomastery.io/courses/learn-vibe-coding/)
- [NA] No testing module is visible in the syllabus summary.

**5. DeepLearning.AI × Replit: "Vibe Coding 101 with Replit"**
- [V via search snippet; page returned 403] Beginner, about 1 h 34 min. 7 video lessons plus 1 graded assignment (PRO). Instructors are Michele Catasta and Matt Palmer (Replit). Learners build a website performance analyzer and a voting app in Replit's cloud IDE, including hosting and sharing. — [DeepLearning.AI](https://www.deeplearning.ai/short-courses/vibe-coding-101-with-replit/); [corporate page](https://corporate.deeplearning.ai/courses/vibe-coding-101-with-replit/information)
- [I] The cloud IDE removes local-setup pain entirely, which is the opposite trade-off from the Czechitas plan (VS Code, Git and a local Python setup on Windows).
- [V] Related: Andrew Ng's "AI Python for Beginners" teaches Python basics (variables, functions, loops, data structures, packages, APIs) for non-developers. It runs about 2 weeks × 10 h and has 4 assignments. It is not about coding agents, but it is a reference point for "Python literacy for non-programmers". — [Class Central listing](https://classcentral.com/course/coursera-ai-python-for-beginners-389372)

**6. Stanford Continuing Studies: TECH 36 A "Vibe Coding: Using AI for Programming"**
- [V] Live online, 5 weekly sessions × 1.5 h (7.5 h), running 24 Sep – 22 Oct 2026 (Thursdays). Price $455. Instructor Ray Villalobos (LinkedIn Learning). Stated audience: "beginners and non-programmers", "no coding experience required". Assessment is NGR, i.e. no grade. Learners should expect $25–$100/month in third-party tool costs. — [Stanford CSP](https://continuingstudies.stanford.edu/courses/professional-and-personal-development/vibe-coding-using-ai-for-programming/20261_TECH-36-A)
- [NA] No detailed weekly syllabus or tool list is public.

**7. Maven live cohorts for non-technical builders (examples)**
- [V] "Claude Code for Beginners: 2 Day Intensive" (Avthar Sewrathan). Two days, about 6 h + 5 h live, plus office hours, a Slack community and a Demo Day. Class 1 covers setup, prompts, CLAUDE.md and multi-platform use. Class 2 covers Skills, Plugins, MCP, spec-driven development, a build loop, and "write tests to ensure your projects work". Requires Claude Pro or Max. Rated 4.9 from 8 reviews; the shown cohort was 14–15 March. The page shows no price and no Git or security content. — [Maven](https://maven.com/alpha-clarity/claude-code-for-beginners)
- [V] "Claude Code Workshop" (Harold Dijkstra, Kieran Ball). 4 h live, with demo/exercise rounds. Tools: Claude Code, Lovable, Supabase, GitHub. Aimed at PMs and marketers; the goal is a "live product". No reviews, price or dates shown. — [Maven](https://maven.com/no-code-ai/claude-code-workshop)
- [V] Maven also lists "Claude Code for Non-Technical Founders and Creators" (4 weeks) and "Claude Code Mastery: From Operator to Builder". These were not fetched. — [Maven search listing](https://maven.com/courses/claude-code)

**8. Free self-paced: Vibe Code School "Claude Code — Vibe Coding"**
- [V] Free, no signup, 28 lessons in 5 modules, built by Dinesh Puppala, assumes zero coding experience. It covers CLAUDE.md and memory; reading, editing and searching a codebase; running tests; Git operations; debugging; slash and custom commands; Skills; subagents; Plan Mode; hooks; MCP; Spec→Tests→Code; "When to Interrupt"; code review; legacy migration; production shipping; and a 60-minute capstone. — [Vibe Code School](https://vibecodeschool.com/courses/claude-code-vibe-coding)
- [I] The topic list is the closest match to the Czechitas syllabus. However, it is a single-author site with no visible publication date, reviews or outcome data, so it is low-evidence.

**9. Other short or minor offerings**
- [V] Codecademy, "Intro to AI Coding with Cursor": under 1 h, one lesson plus a quiz, free (certificate needs Plus or Pro). — [Codecademy](https://www.codecademy.com/learn/intro-to-ai-coding-with-cursor)
- [V] DataCamp, "Vibe Coding with Replit": about 2–3 h, with a ~$25/month subscription. It builds a Typeform-style clone with auth and deployment. The source is DataCamp's own blog (dated 15 Jul 2026), so it is self-promotional. — [DataCamp blog](https://www.datacamp.com/blog/best-vibe-coding-course-for-non-technical-founders)
- [V] Udemy examples:
  - "Vibe Coding for Non Coders": 4.4 from 76 reviews, 3,407 students, per a search snippet. — [Udemy](https://www.udemy.com/course/vibe-coding-for-non-coders/)
  - "Vibe Coding to Claude Code Mastery": listed as updated April 2026, per a search snippet. — [Udemy](https://www.udemy.com/course/vibe-coding-to-claude-code-mastery-build-ai-apps-agents/)
  - Neither page was fetched; treat their ratings skeptically.
- [V] Anthropic Academy, "Claude Code in Action": free, Intermediate, about 1 h of video and 1 quiz, aimed at software engineers. Excluded as not beginner-oriented. Source is a secondary summary, not the Skilljar page. — [pasqualepillitteri.it summary](https://pasqualepillitteri.it/en/news/371/anthropic-academy-free-courses-claude)

**10. Czech offerings**
- [V] Czechitas, "Vibe coding v praxi: vytvoř si vlastní web s AI bez programování":
  - 28 h over 6 sessions in 2 weeks, aimed at non-programmers.
  - Tools: Macaly (free PRO access provided), Git, Vercel.
  - Syllabus: HTML/CSS/JS basics, code reading and modification, debugging, Git, and web deployment, ending with the learner's own deployed web app.
  - Price 21,990 CZK full, 7,490 CZK discounted. Certificate at 80% attendance.
  - The date shown (29 Sep – 10 Oct) may refer to a past run; the year was not confirmed.
  - Source: [Czechitas](https://www.czechitas.cz/kurzy/vibe-coding-v-praxi-vytvor-si-vlastni-web-s-ai-bez-programovani)
- [V] Czechitas, "Vibe coding: jak začít tvořit aplikace pomocí AI": a 2 h intro workshop on clickable prototypes with AI design tools. Free for women, otherwise 390–590 CZK. Listed dates are in Nov/Dec 2025, so the page may be stale. — [Czechitas](https://www.czechitas.cz/kurzy/vibe-coding-jak-zacit-tvorit-aplikace-pomoci-ai)
- [V] Engeto, "Web Developer Akademie":
  - 250+ h over 14–17 weeks; live online on Thursdays 18:00–21:00. Next start 19 Nov 2026.
  - Covers full-stack JS (Node, Express, PostgreSQL), uses Cursor, and teaches "critical evaluation of AI-generated solutions". Git/GitHub, deployment and security basics are included.
  - Price 25,990 CZK (36,990 list), with possible 77% subsidy via "Jsem v kurzu".
  - It is a traditional coding academy with AI, not agent-first.
  - Source: [Engeto](https://engeto.cz/webova-akademie/)
- [V] Engeto also runs an "AI Akademie" (17 weeks, 51+ h, from Nov 2026) that includes vibe coding and custom AI assistants. This is a search snippet only and was not fetched. — [Engeto AI kurzy](https://engeto.cz/ai-kurzy/)
- [NA] No agentic-coding course was found for Green Fox or Coding Bootcamp Praha, but this was a single search and not exhaustive.

### Inferences
- [I] The market splits into two groups. The first is tool-feature tours (Scrimba Claude Code, Maven intensives, Vibe Code School), which cover CLAUDE.md, Skills, MCP, hooks and subagents. The second is "direct and verify" mental-model courses (Vanderbilt), which deliberately avoid Git and the terminal. Few combine both with real engineering literacy.
- [I] Python code reading for non-programmers appears in none of the agent courses. Where code literacy appears at all (Czechitas Vibe coding v praxi, ZTM, Engeto), it is HTML/CSS/JS.
- [I] Hands-on work on an existing codebase is rare. The only visible examples are Scrimba's "Exploring a Codebase" video and Vibe Code School's "Legacy Migration" lesson. Nearly all projects are greenfield.

### Gaps
- Exact current prices for the Coursera items (depend on region and Plus), the Maven courses (not shown on the fetched pages), and DeepLearning.AI PRO.
- DeepLearning.AI lesson list (HTTP 403).
- Completion and outcome data: none published by any provider.

## Detailed topic coverage of the strongest offerings (mentioned vs practiced vs assessed)

### Takeaway
Vanderbilt's "Build Apps with AI" is strongest on verification thinking (silent failures, real-data testing, user journeys turned into tests), but these topics are readings and videos only, not assessed. Scrimba/Coursera "Vibe Coding with Claude Code" is strongest on agent mechanics. ZTM is strongest on environment setup. Czechitas "Vibe coding v praxi" is the closest format match (28 h live, Git, deployment). Every course is weak on independent verification, deliberate failure-and-recovery exercises, secrets and prompt-injection security, and model/cost selection.

### Cited Findings
Coverage matrix (M = mentioned/taught on syllabus, P = named exercise or assignment, A = graded, — = not visible in public syllabus):

| Topic | Vanderbilt Build Apps | Scrimba Claude Code (Coursera) | ZTM Bootcamp | Vibe Code School | Czechitas Vibe coding v praxi | Maven 2-day intensive |
|---|---|---|---|---|---|---|
| Code reading / literacy | — | — | M (HTML/JS) | M | M (HTML/CSS/JS) | — |
| Env setup & terminal | — | M (setup) | M (terminal, VS Code, Node) | M (install CLI) | — | M |
| Requirements / acceptance criteria | M (Before/After, Design First), A (2 builds) | M (Plan Mode) | M ("Director") | M (Spec→Tests→Code) | M (app design) | M (spec-driven) |
| Context / instruction files | M (context folder) | M (rules, context window, Skills) | M (MCP) | M (CLAUDE.md, Skills) | — | M (CLAUDE.md, Skills) |
| Git / diff / rollback | — | M (checkpoints, worktrees, PRs) | M (Git/GitHub) | M (Git ops, code review) | M (Git) | — |
| Debugging / agent failures | M (Silent Failure Audit) | M (bugs) | — | M (debugging, "When to Interrupt") | M (debugging) | — |
| Testing | M (real data, user journeys → automated tests, visual testing) | M ("Bugs, Refactoring, and Tests") | — | M (running tests, tests-first) | M (user testing, workshop only) | M ("write tests") |
| Independent verification beyond agent's own tests | M (real data, silent failures) | — | — | M (code review) | — | — |
| MCP / subagents / hooks | — | M (all three) | M (MCP) | M (all three) | — | M (MCP, plugins) |
| Security | M (one reading) | M ("Security Checks") | — | — | — | — |
| Deployment / maintenance | M (maintenance reading) | — | P (portfolio deploy, inferred) | M ("Production Shipping") | P (Vercel deploy of own app) | P (Demo Day) |
| Model selection & cost | M (AI labor economics, in the sister Claude Code course) | — | M (choosing an AI partner; Ollama) | — | — | — |

Sources: [Vanderbilt Build Apps](https://www.coursera.org/learn/build-apps-with-ai); [Scrimba Claude Code](https://www-cloudfront-alias.coursera.org/learn/introduction-to-claude-code); [ZTM](https://zerotomastery.io/courses/learn-vibe-coding/); [Vibe Code School](https://vibecodeschool.com/courses/claude-code-vibe-coding); [Czechitas](https://www.czechitas.cz/kurzy/vibe-coding-v-praxi-vytvor-si-vlastni-web-s-ai-bez-programovani); [Maven](https://maven.com/alpha-clarity/claude-code-for-beginners); [Vanderbilt Claude Code](https://www.coursera.org/learn/claude-code)

Teaching approach (as visible):
- [V] Vanderbilt uses a short-video plus reading plus AI-graded "bring your own data/workflow" assignment pattern. Learners build tools for their own job ("Build a Web App for Your Own Workflow", expense analyzer, dashboards). The course recommends Claude Code, Cowork and MAJK, but the visible syllabus has no setup walkthrough. — [Coursera](https://www.coursera.org/learn/build-apps-with-ai)
- [V] Setup pain is avoided entirely in two ways: Replit/DLAI and DataCamp use a cloud IDE, and Czechitas "v praxi" uses the Macaly platform. — [DLAI](https://www.deeplearning.ai/short-courses/vibe-coding-101-with-replit/); [DataCamp blog](https://www.datacamp.com/blog/best-vibe-coding-course-for-non-technical-founders); [Czechitas](https://www.czechitas.cz/kurzy/vibe-coding-v-praxi-vytvor-si-vlastni-web-s-ai-bez-programovani)
- [V] ZTM and the Maven intensive address setup head-on, with a dedicated setup module and optional setup-help sessions respectively. — [ZTM](https://zerotomastery.io/courses/learn-vibe-coding/); [Maven](https://maven.com/alpha-clarity/claude-code-for-beginners)
- [V] Maven formats use live demo → hands-on rounds → Demo Day. — [Maven workshop](https://maven.com/no-code-ai/claude-code-workshop); [Maven intensive](https://maven.com/alpha-clarity/claude-code-for-beginners)

### Inferences
- [I] No course visibly uses deliberately flawed agent output or a planted bug for recovery practice. Vanderbilt's "Silent Failure Audit" comes closest, conceptually. This is a differentiation opportunity for Czechitas ("tests pass ≠ requirement met").
- [I] No offering visibly assesses Git-based review or rollback. Graded work everywhere is "did you build something", and on Coursera it is AI-graded.
- [I] Windows/PowerShell support is not addressed on any landing page.

### Gaps
- Actual exercise content, rubrics and feedback quality are paywalled for every course; the AI-graded rubric format on Coursera is not public.
- No public exercise GitHub repos were found for these courses (not exhaustively searched).

## Evidence of quality beyond marketing

### Takeaway
Credible independent evidence is thin. Ratings come from platforms, are small-n for the new agent-specific courses, and are sometimes inflated by bundling. No outcome or completion data and no substantive independent reviews (Reddit, HN, Class Central critiques) were found.

### Cited Findings
- [V] Rating sample sizes for the agent-specific courses are small:
  - Vanderbilt "Build Anything with AI": 4.2 from 13 reviews. — [Coursera](https://www-cloudfront-alias.coursera.org/learn/build-anything-with-ai)
  - Scrimba "Vibe Coding with Claude Code": 4.5 from 30 reviews, with 67% five-star. — [Coursera](https://www-cloudfront-alias.coursera.org/learn/introduction-to-claude-code)
  - Maven intensive: 4.9 from 8 reviews. — [Maven](https://maven.com/alpha-clarity/claude-code-for-beginners)
- [V] Specialization ratings (4.8 from 8k–9.6k reviews) exceed enrollment counts, which indicates they aggregate older bundled courses. — [Coursera spec](https://www-cloudfront-alias.coursera.org/specializations/build-anything-with-ai)
- [V] Most "best vibe coding course" pages found are listicles or vendor blogs, which the brief excludes as evidence. Example: DataCamp ranks its own course first. — [DataCamp blog](https://www.datacamp.com/blog/best-vibe-coding-course-for-non-technical-founders)
- [V] Freely previewable content: Vibe Code School is fully free with no signup, and the Coursera courses offer free enrollment or audit for the videos (Coursera AI Builder says it cannot be audited free). — [Vibe Code School](https://vibecodeschool.com/courses/claude-code-vibe-coding); [Coursera AI Builder](https://www.coursera.org/specializations/ai-builder)

### Inferences
- [I] For a deeper benchmark, the most informative next step would be to audit the free Coursera videos of "Build Apps with AI", Module 4 (testing), and the Scrimba Claude Code Module 2 lesson "Bugs, Refactoring, and Tests".

### Gaps
- No completion rates, job or outcome data, or independent critiques were found for any listed course.
- Reddit and HN searches returned no substantive threads on these specific courses within the search budget.
