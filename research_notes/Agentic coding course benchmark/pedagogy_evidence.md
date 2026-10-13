# Evidence base: teaching novices to program and build software with generative AI / coding agents (research date 2026-10-07)

Evidence-strength labels used below: **RCT** (randomized controlled trial), **controlled experiment** (lab study with conditions, not necessarily randomized at scale), **field/course report** (one course offering, usually pre/post or historical comparison), **survey**, **qualitative** (interviews, observation, think-aloud; small n), **corpus analysis** (mining artifacts), **opinion/design proposal**. "Verified this session" means the claim was read from a search result or the fetched source during this research; items marked "(from prior knowledge, URL not re-fetched)" should be spot-checked before citing in final materials.

General caveat: almost all CS-education studies concern university CS1 students or K-12 learners using chat assistants or autocomplete (Copilot/Codex), not adult non-programmers directing autonomous agents (Claude Code, Codex CLI). Direct evidence on the course's exact population is thin; most course-design guidance is inference by transfer.

## 1. Novices' metacognitive difficulties, over-reliance and the "illusion of competence"

### Takeaway
The strongest single theme in the literature: AI helps already-capable learners and can harm struggling ones, who cannot tell good suggestions from bad and overestimate their understanding. Controlled studies (including two RCTs) show that *how* AI is used matters more than *whether*: delegating code generation lowers learning, while using AI to ask conceptual questions or as a guarded tutor preserves it.

### Cited Findings
- **Prather et al., "The Widening Gap" (ICER 2024)** — qualitative (21 lab sessions with observation, interviews, eye tracking). Students who were already doing well used GenAI to speed up code they already intended to write and ignored bad suggestions; struggling students kept their old metacognitive difficulties, and GenAI made them worse and added new ones. The new difficulties were being "interrupted" by constant suggestions, being "misled" down wrong paths, and a lack of "progression" from over-reliance. Students also overestimated their understanding. Small n, single institution. — [arXiv 2405.17739](https://arxiv.org/abs/2405.17739v1); [ICER 2024 listing](https://icer2024.acm.org/details/icer-2024-papers/26/The-Widening-Gap-The-Benefits-and-Harms-of-Generative-AI-for-Novice-Programmers)
- **Anthropic skill-formation RCT (Jan 2026)** — RCT, n=52 professional Python developers learning an unfamiliar library (Trio). The AI group averaged about 50% on a follow-up quiz vs about 67% for hand-coders. The time saved (about 2 minutes) was not statistically significant. The largest deficit was on **debugging** questions. Participants who used AI for conceptual questions scored ≥65%; those who delegated code generation scored <40%. Industry-run, small n, short task, but randomized. — [Anthropic research page](https://www.anthropic.com/research/AI-assistance-coding-skills); [arXiv 2601.20245](https://www.arxiv.org/pdf/2601.20245); [InfoQ summary](https://infoq.com/news/2026/02/ai-coding-skill-formation/)
- **Bastani et al., PNAS 2025** — field RCT, about 1,000 high-school math students (Turkey). It is not a programming study but is the best-powered evidence on "AI as a crutch". With access, practice performance rose 48% (plain GPT-4) and 127% (guard-railed "GPT Tutor"). Once access was removed, the plain-GPT group scored **17% worse** than controls. Guardrails largely removed the harm. — [CHIBE/UPenn](https://chibe.upenn.edu/publications/generative-ai-without-guardrails-can-harm-learning-evidence-from-high-school-mathematics); [SSRN](https://papers.ssrn.com/abstract=4895486); [RePEc PNAS record](https://ideas.repec.org/a/nas/journl/v122y2025pe2422633122.html)
- **Contractor & Reyes (arXiv July 2026)** — proctored RCT with undergraduates, using an essay task (not coding). AI access raised test scores, and a smaller gain lasted a week. Gains held for "augmentation" use (AI as tutor) and faded for "automation" use (AI writes the essay). — [arXiv 2607.08849](https://arxiv.org/abs/2607.08849)
- **Kazemitabaar et al. (CHI 2023)** — RCT, 69 learners aged 10–17 over 10 sessions. Codex access raised task completion (1.15x) and scores (1.8x) without hurting later manual code-modification performance. On retention one week later, the Codex group did slightly better, but not significantly. Learners with higher prior (Scratch) skill benefited more, which matches the "widening gap" finding. — [arXiv 2302.07427](https://arxiv.org/abs/2302.07427v1)
- **METR RCT on experienced developers (July 2025)** — RCT, 16 experienced open-source maintainers, 246 tasks, Cursor plus Claude 3.5/3.7. Developers were **19% slower** with AI, yet believed afterwards that they had been about 20% faster (they forecast 24% faster beforehand). This is the cleanest evidence that self-perceived productivity with AI is unreliable even for experts. Small n, specific setting (mature repos the developers knew well), early-2025 tools. — [METR blog](https://metr.org/blog/2025-07-10-early-2025-ai-experienced-os-dev-study/) (from prior knowledge, URL not re-fetched); [Simon Willison summary](https://simonwillison.net/2025/Jul/12/ai-open-source-productivity/); [InfoQ](https://www.infoq.com/news/2025/07/ai-productivity)
- **Perry et al. (CCS 2023)** — controlled user study (about 47 participants; from prior knowledge). Participants with an AI assistant wrote significantly less secure code **and were more likely to believe their code was secure**. Participants who put more work into their prompts (adding helper context, adjusting parameters) were more likely to produce secure solutions. — [arXiv 2211.03622](https://arxiv.org/abs/2211.03622v1)

### Inferences
- The overconfidence effect appears in a pattern across populations: novices (Prather), experts' productivity (METR), and security (Perry). The course should **make calibration an explicit learning goal**: learners predict whether the agent's change works before checking, then compare.
- Because the learners are "ChatGPT power users", they are likely to arrive with the delegation habit that the Anthropic and Bastani studies tie to weaker learning. Early exercises should require learners to ask the agent *explain/why* questions and to make their own predictions, not just *do it* requests.
- The "widening gap" implies that weaker learners need more structure (checklists, guarded prompts, pairing), not less. A "just let the agent do it" phase will mostly hurt them.

### Gaps
- No RCT found on adult non-programmers using autonomous coding agents (Claude Code/Codex CLI) and measuring learning. Every causal evidence item above concerns chat/autocomplete tools, other domains, or professionals.
- METR published follow-up work in late 2025/2026 with newer tools. I did not retrieve it, so whether the slowdown persists with 2026 agents is unverified here.

## 2. Code reading/tracing before writing (PRIMM, Parsons, explain-in-plain-English), prompt problems, and scaffolding that works

### Takeaway
Pre-AI evidence for "read before write" (PRIMM, Parsons problems, subgoal-labelled worked examples) is solid and directly relevant now that learners' main job is reading generated code. The AI-era evidence adds a sobering result: beginners understand LLM-generated code poorly (about 32% success), and their prompts fail because they leave out *information*, not because of vocabulary. New exercise types (Prompt Problems) and guarded tutors (CodeHelp, CS50 duck) are well received, but their learning-outcome evidence is mostly surveys.

### Cited Findings
- **PRIMM (Predict–Run–Investigate–Modify–Make)**, Sentance et al. The framework addresses novices trying to write before they can read. The original multi-school study (Sentance, Waite & Kallia, *Computer Science Education* 2019; about 490 students aged 11–14, quasi-experimental) found PRIMM classes outperformed comparison classes on a post-test (from prior knowledge). — [Raspberry Pi Foundation PRIMM seminar slides](https://www.raspberrypi.org/app/uploads/2022/08/Teaching_Programming_with_PRIMM-1.pdf); [NCCE PRIMM quick read](https://static.teachcomputing.org/pedagogy/QR11-PRIMM.pdf); [Sentance et al. 2019, T&F](https://www.tandfonline.com/doi/full/10.1080/08993408.2019.1608781) (from prior knowledge, URL not re-fetched)
- **Parsons problems** — controlled experiments (Ericson et al.). On 30-minute labs they saved 15–17 minutes (43.6–65.2% of time), and students did equally well on later assignments compared with writing code from scratch. **Subgoal labels** in worked examples improved performance over no labels or self-generated labels. — [Raspberry Pi subgoal-labels seminar (Margulieux)](https://www.raspberrypi.org/app/uploads/2020/07/Using-subgoal-labels-to-reduce-cognitive-load-in-introductory-programming.pdf); [guided Parsons + subgoals, arXiv 2505.04712](https://arxiv.org/pdf/2505.04712)
- **Zi et al., "I Would Have Written My Code Differently" (2025)** — controlled study, 32 CS1 students, 160 task instances. Students judging what LLM-generated code does succeeded on only **32.5%** of tasks. Barriers were unfamiliar Python syntax and style, automation bias (assuming the code is correct), and extra difficulty for non-native English speakers. — [arXiv 2504.19037](https://arxiv.org/pdf/2504.19037); [author page](https://www.khoury.northeastern.edu/~arjunguha/main/papers/2025-zi-reverse-charlie.html)
- **Nguyen et al., "How Beginning Programmers and Code LLMs (Mis)read Each Other" (CHI 2024)** — controlled study, 120 beginners across 3 institutions. Beginners struggled to write and edit prompts even for problems at their own skill level, and even with automatic correctness feedback. — [arXiv 2401.15232](https://arxiv.org/html/2401.15232v2)
- **"Substance Beats Style" (2024)** — analysis of the same project's prompts. Prompt success is predicted by the *information content* (whether necessary details are stated), not by technical vocabulary. Students do not know what the model can infer and what they must state. — [arXiv 2410.19792](https://arxiv.org/html/2410.19792v1)
- **Prompt Problems (Denny, Leinonen, Prather et al., SIGCSE 2024)** — design plus classroom deployment (survey/qualitative). Students see a *visual* problem description and must write a prompt whose generated code passes tests. The exercise trains specifying behaviour precisely without copy-pasting the task text. Tool: Promptly. — [arXiv 2311.05943 / SIGCSE listing](https://sigcse2024.sigcse.org/details/sigcse-ts-2024-Papers-1/63/Prompt-Problems-A-New-Programming-Exercise-for-the-Generative-AI-Era); [follow-up arXiv 2401.10759](https://arxiv.org/abs/2401.10759v1)
- **CodeHelp (Liffiton, Sheese, Savelka, Denny, Koli Calling 2023)** — pilot deployment (usage logs plus survey). An LLM helper with guardrails withholds solution code. 95% of students wanted to use it again, at about $0.002 per query. The code-removal guardrail mostly worked but sometimes explained concepts not yet taught. — [arXiv 2308.06921](https://arxiv.org/abs/2308.06921v1); [Gen-Ed open source](https://github.com/liffiton/Gen-Ed)
- **CS50 duck (Liu, Malan et al., SIGCSE 2024)** — course report. A guard-railed tutor gives hints rather than answers. Asynchronous Q&A submissions dropped by 75%. Outcomes are adoption and satisfaction, not learning gains. — [Harvard PDF](https://cs.harvard.edu/malan/publications/V1fp0567-liu.pdf); [CS50.ai docs](https://cs50.readthedocs.io/cs50.ai/)
- **Kazemitabaar et al., CodeAid (CHI 2024)** — semester deployment, about 700 students (from prior knowledge). Students valued an assistant that gave pseudo-code and explanations instead of direct solutions. Educators wanted it to avoid revealing full code. — [arXiv 2401.11314](https://arxiv.org/abs/2401.11314) (from prior knowledge, URL not re-fetched)
- **Prather et al., ITiCSE 2023 working group "The Robots are Here"** — literature review plus surveys of instructors and students. It recommends adapting curricula toward code reading, evaluation and specification instead of banning AI. — [arXiv 2310.00658](https://arxiv.org/abs/2310.00658) (from prior knowledge, URL not re-fetched)

### Inferences
- For a course whose goal is "recognise and reason about generated code", PRIMM's *Predict* and *Investigate* steps map directly onto reviewing an agent's diff. Learners predict what the change will do, run it, then step through it in the debugger. This supports **integrating code literacy throughout** in short PRIMM cycles on *agent-generated* code, instead of front-loading two generic Python lectures that delay the course's real activity. A middle path: a compact Python "reading kit" in lectures 1–2 (variables, if, loops, functions, exceptions, read via Parsons/predict tasks), then recurring 15–20 minute code-reading drills on the learner's own agent output in every later lecture.
- The 32.5% comprehension rate is a warning that reading AI code is *harder* than reading textbook code (unfamiliar idioms). Teaching materials should include "explain this generated function in plain English" tasks and allow learners to ask the agent to simplify its code.
- Prompt Problems and "Substance beats style" suggest teaching **specification content checklists** (inputs, outputs, edge cases, constraints, acceptance criteria) instead of "prompt-engineering tricks".

### Gaps
- No study found that directly compares "front-load Python" vs "integrate Python" in an AI-first course. The recommendation above is inference.
- No published evidence that PRIMM transfers to multi-file agent diffs (Django apps). Existing studies use short single programs.

## 3. Teaching code review, testing and verification; specification and acceptance-criteria skills

### Takeaway
Novices struggle most with writing acceptance criteria detailed enough to test, and with fixing AI-generated code. LLMs can help them draft criteria. No study was found that directly measures "tests pass but test the wrong requirement" in novices, though the mechanism (automation bias plus weak specifications) is well documented.

### Cited Findings
- **LLM impact on student user stories and acceptance testing (2025)** — classroom experiment. Students found it hardest to write acceptance criteria detailed enough to derive test cases. LLM assistance raised acceptance-criteria scores by **88%** (statistically significant). — [arXiv 2502.02675](https://arxiv.org/pdf/2502.02675)
- Students found **correcting LLM-generated code** in exams significantly harder than instructor-designed tasks (exam study, *International Journal of AI in Education* 2025). — [Springer s40593-025-00496-4](https://link.springer.com/article/10.1007/s40593-025-00496-4)
- Automation bias, meaning beginners assume generated code is correct, was a named failure cause in the comprehension study. — [arXiv 2504.19037](https://arxiv.org/pdf/2504.19037)
- **Fawzy, Tahir & Blincoe, "From Prompting to Verification" (2026)** — survey, n=162 (non-developers, novices, professionals). Risk awareness about AI code was widespread across groups, but non-developers and novices did not verify systematically. The authors call this a "perception–action gap". — [Emergent Mind summary of arXiv 2605.24521](https://www.emergentmind.com/papers/2605.24521)
- **Agentic PR studies (professional context)** — corpus analysis. Of 567 Claude Code-generated PRs in 157 OSS projects, 83.8% were merged, but **45.1% of merged PRs needed human revision**, especially bug fixes, documentation, and project conventions. — [arXiv 2509.14745](https://arxiv.org/pdf/2509.14745). A comparison of 7,156 PRs from 5 agents found that acceptance and review burden varied by agent and task type. — [arXiv 2602.08915](https://arxiv.org/html/2602.08915v1); see also [Why agentic PRs get rejected, arXiv 2602.04226](https://arxiv.org/html/2602.04226v1)

### Inferences
- The course memory's emphasis that "passing tests does not guarantee the original requirement" fits the evidence well. A concrete exercise: learners write acceptance criteria first, the agent writes code *and* tests, and learners audit which criteria are actually covered. Seeding a requirement-misreading bug where tests still pass would make the point memorable.
- The agentic PR data gives realistic numbers for learners: even in professional settings, about half of accepted agent PRs needed human edits.

### Gaps
- No empirical study found specifically on novices detecting tests that verify the wrong requirement. This is a research gap; treat the point as practitioner wisdom.
- No controlled study found on teaching *diff review* to non-programmers.

## 4. Cognitive load and setup friction (environment setup, cloud vs local, worked examples, fading)

### Takeaway
Installation and configuration are consistently reported as the first major barrier for novices, and cloud environments are a common remedy. The evidence is mostly experience reports, not controlled studies. Cognitive-load research supports worked examples with subgoals, Parsons problems, and gradual fading of support.

### Cited Findings
- Installation and configuration are described as the most common hurdle when starting computation. Differences in OS, versions and configurations make universal instructions impossible (experience report, intro data science). — [arXiv 2008.00315 "A fresh look at introductory data science"](https://arxiv.org/pdf/2008.00315)
- ETH Zurich's 14-year software engineering course report states that setting up a development environment is a constant source of trouble that can be "terrifying" for novices, and motivates browser-based Codeboard. — [arXiv 1712.05078](https://arxiv.org/pdf/1712.05078)
- Kingston University paper on "Computer says no", about reducing technical barriers for novice programmers (paper exists; content not read). — [Kingston research portal](https://researchinnovation.kingston.ac.uk/en/publications/computer-says-no-reducing-technical-barriers-to-help-novice-progr/)
- The Parsons-problem and subgoal-label evidence in Section 2 is the main cognitive-load evidence (controlled experiments). — [Margulieux subgoals](https://www.raspberrypi.org/app/uploads/2020/07/Using-subgoal-labels-to-reduce-cognitive-load-in-introductory-programming.pdf)

### Inferences
- With mostly Windows/PowerShell learners and three moving parts (VS Code, Git, an agent CLI with auth), setup is a likely early dropout point. Options: (a) a cloud environment such as GitHub Codespaces for lectures 1–2, then local setup later *with the agent's help* (which also demonstrates "agents help with setup"); or (b) a pre-course setup clinic with a checked install script. Choosing (a) matches the evidence trend but adds an account and quota dependency to verify.
- Fading plan: instructor live-demo → guided worked example with subgoal labels → paired task with checklist → independent task with only acceptance criteria given. This follows the worked-example and fading literature (inference; no AI-agent-specific study found).

### Gaps
- No quantitative study found linking setup friction to dropout in adult/bootcamp courses. Claims rest on experience reports.
- No study found comparing Codespaces/cloud vs local installs for agentic-coding courses.

## 5. Professional-developer and security evidence relevant to what beginners must check

### Takeaway
Generated code is often insecure, users with AI are overconfident about security, models invent package names that attackers can register, and even experts misjudge AI's speedup. These give a concrete "what to check" list for beginners.

### Cited Findings
- **Pearce et al., "Asleep at the Keyboard?" (IEEE S&P 2022)** — systematic generation study. About 40% of 1,689 Copilot-generated programs in security-relevant scenarios contained CWE vulnerabilities (from prior knowledge). — [arXiv 2108.09293](https://arxiv.org/abs/2108.09293) (URL not re-fetched)
- **Perry et al. (CCS 2023)** — controlled user study. Less secure code with AI, combined with higher confidence. — [arXiv 2211.03622](https://arxiv.org/abs/2211.03622v1)
- **Spracklen et al., package hallucinations (USENIX Security 2025)** — 16 models, 576,000 code samples. **19.7%** of recommended packages did not exist (205,474 unique fake names). 43% of hallucinated names recurred across repeated prompts, which makes "slopsquatting" (registering those names as malware) practical. — [arXiv 2406.10279](https://arxiv.org/abs/2406.10279) (URL from prior knowledge); [CSA research note 2026](https://labs.cloudsecurityalliance.org/research/csa-research-note-slopsquatting-ai-supply-chain-20260419-csa/)
- **METR RCT** — 19% slower, but perceived 20% faster (see Section 1). — [Simon Willison summary](https://simonwillison.net/2025/Jul/12/ai-open-source-productivity/)
- **Agentic PRs** — 45% of merged Claude Code PRs needed human changes (see Section 3). — [arXiv 2509.14745](https://arxiv.org/pdf/2509.14745)

### Inferences
- Beginner checklist derived from this evidence: verify that every new dependency exists and is the intended package (check PyPI page, downloads, repository); never commit secrets; check auth and permission logic; run the app and tests yourself; inspect the diff before committing; distrust your own feeling of "it works".
- The METR result is useful in class to show that "feeling productive" is not evidence.

### Gaps
- No data found on security outcomes for non-programmers deploying vibe-coded apps (2025–2026 incident reports exist in press, but none were collected here).

## 6. Assessment approaches for AI-assisted programming courses (judgment, integrity)

### Takeaway
The field is converging on oral and interactive assessment (code interviews, conversational exams, walkthroughs) and on large projects, because take-home code output no longer shows understanding. The evidence is mostly design reports and small evaluations.

### Cited Findings
- **Code Interviews (SIGCSE 2025)** — design and evaluation in an intro course. Short interviews about take-home assignments are a more authentic assessment and address integrity concerns. — [arXiv 2410.01010](https://arxiv.org/html/2410.01010v2)
- **Conversational Exam (2026)** — field report, 58 students in small groups over two days. Students code live while explaining their reasoning, and the authors argue the format scales. — [arXiv 2601.10691](https://arxiv.org/pdf/2601.10691)
- **AI-driven oral exams (SIGCSE 2026 lightning talk)** — an automated conversational tool probes students' understanding of their own submissions (Classmoji). Early-stage. — [SIGCSE 2026 listing](https://sigcse2026.sigcse.org/details/sigcse-ts-2026-lightning-talks/17/AI-Driven-Oral-Examinations-for-Code-Assessment-Evaluating-Understanding-Beyond-the-)
- **UCSD CS1-LLM** — large open-ended projects were judged especially valuable in the LLM context. — [arXiv 2510.18806](https://arxiv.org/abs/2510.18806)
- Practitioner guide (MIT) on alternative assessments for the AI era (opinion). — [MIT post](https://www.mit.edu/~edchen93/posts/design-programming-courses-ai-era-assessment)

### Inferences
- For a non-credit 10-lecture course, a light version could work: (1) a **process log** per task (prompt, what the agent did, what I checked, what I rejected and why); (2) a **5-minute walkthrough** of the capstone diff, where the learner explains one function, one test, and one decision they overrode; (3) a **judgment rubric** scoring specification quality, verification evidence, appropriate rejection of agent output, and Git hygiene, not feature count.
- "Seeded-fault" tasks, where the agent output contains a known bug or security flaw, assess judgment directly. This is inference; I found no validated instrument.

### Gaps
- No validated rubric for "judgment in agentic coding" was found.
- No studies found on reflection logs specifically in AI-assisted programming courses (they exist for general programming).

## 7. Vibe coding / agentic coding by non-programmers and novices (2025–2026)

### Takeaway
Early studies (a hackathon, a prompt-log study, a survey) agree that vibe coding enables fast prototyping and motivation but produces uneven quality, little engagement with engineering practices (testing, version control), and weak verification by non-experts. More experienced students give the AI more relevant context.

### Cited Findings
- **"Can you feel the vibes?" (arXiv Dec 2025)** — qualitative, one-day hackathon, 31 undergraduates (computing and non-computing) in Brazil. Benefits were rapid prototyping, cross-disciplinary collaboration, and growing prompt skills. Problems were premature convergence on ideas, uneven code quality requiring rework, and **limited engagement with core software engineering practices**. — [arXiv 2512.02750](https://arxiv.org/abs/2512.02750v1)
- **"Exploring Student-AI Interactions in Vibe Coding" (arXiv 2025)** — qualitative/prompt analysis. Advanced SE students' prompts were much more likely to include relevant app-feature and codebase context than introductory students' prompts. — [arXiv 2507.22614](https://arxiv.org/html/2507.22614v2)
- **Fawzy, Tahir & Blincoe (2026)** — survey, n=162. Non-developers come for accessibility; they are aware of risks but verify least systematically. — [Emergent Mind summary](https://www.emergentmind.com/papers/2605.24521)

### Inferences
- Since the course memory's learners match the "non-developer" profile, the main teaching risk is a *perception–action gap*: they will know they should verify but won't. Verification must be a required, graded ritual (checklist plus commit gate), not advice.
- Explicitly teaching learners to give the agent **context** (which file, which feature, constraints, project instruction files like AGENTS.md) addresses the novice/advanced difference seen in 2507.22614.

### Gaps
- No longitudinal study found on non-programmers learning over multiple weeks with Claude Code/Codex-style agents.
- No studies found on Git learning by non-programmers mediated by agents.

## 8. Course redesigns reported by universities and their outcomes

### Takeaway
UCSD's CS1-LLM is the best-documented redesign. It shifted outcomes toward problem decomposition, code reading, testing and debugging while using Copilot from week 1. Exam performance was comparable to historical cohorts, and students viewed the tools favourably while worrying about dependence. Other notable redesigns (CS50 duck, Stanford CS146S) report adoption or curriculum, not learning outcomes.

### Cited Findings
- **Vadaparty et al., CS1-LLM (ITiCSE 2024)** — course report. Learning goals were reprioritised (decomposition, reading, testing, debugging over syntax writing). Almost 80% of students were comfortable programming with GenAI, and almost 60% felt it improved their conceptual understanding (survey). — [arXiv 2406.15379](https://arxiv.org/pdf/2406.15379)
- **Vadaparty et al., outcomes paper (arXiv Oct 2025)** — course report with historical comparison. Exam performance was comparable to historical cohorts; demographic gaps persisted at similar levels. Large open-ended projects were seen as particularly valuable, and students were favourable but worried about over-dependence. — [arXiv 2510.18806](https://arxiv.org/abs/2510.18806)
- The redesign's companion book is Porter & Zingaro, *Learn AI-Assisted Python Programming* (Manning; 2nd ed. 2024), which teaches code reading, testing, and problem decomposition alongside Copilot (from prior knowledge). — [Leo Porter publications](https://leoporter.ucsd.edu/publications/); [AAC&U Academic Minute, Porter 2025](https://www.aacu.org/podcasts/academicminute/2025-05-leo-porter-university-of-california-san-diego-computer-programming-in-the-generative-ai)
- **CS50 (Harvard)** — guard-railed AI duck. 75% fewer asynchronous questions, high adoption; no learning-gain measure. — [Harvard PDF](https://cs.harvard.edu/malan/publications/V1fp0567-liu.pdf)
- **Stanford CS146S "The Modern Software Developer" (Fall 2025, Mihail Eric)** — 10-lecture course covering prompting, agent anatomy/MCP, context engineering, security, code review, and shipping. Assignments include running agents from a design document and security-scanning one's own code. Materials are public, but the audience is CS students and no outcome data was found. — [Stanford bulletin](https://bulletin.stanford.edu/courses/2274401); [course site themodernsoftware.dev](https://themodernsoftware.dev) (URL from search snippet, not fetched)

### Inferences
- CS146S's ten-lecture structure is a useful structural benchmark, but it assumes programming background. The UCSD model (read, test, debug from day one with AI) is the closer pedagogical analogue for non-programmers.
- "Comparable exam outcomes" at UCSD suggests that integrating AI from week 1 does not necessarily harm basic competence *when* the curriculum explicitly teaches reading and testing. That condition matters (inference from Sections 1–2).

### Gaps
- No outcome data found for CS146S or for bootcamp/non-credit agentic-coding courses for non-programmers.
- Lau & Guo (ICER 2023, instructor interviews on AI in intro programming) was not re-verified in this session.

## Summary of design implications (all inference, grounded in the findings above)
1. **Integrate code literacy throughout**, with a short front-loaded "reading kit". Use PRIMM-style predict, run, investigate cycles on agent output in every lecture, plus Parsons/explain-in-plain-English drills. Avoid two lectures of generic syntax before any agent use. (Sections 2 and 8)
2. **Demonstration → independence via fading**: live demo → subgoal-labelled worked example → paired task with checklist → independent task with acceptance criteria only. (Sections 2 and 4)
3. **Make verification compulsory and visible**: acceptance criteria first, an audit of which criteria the tests cover, seeded-fault exercises, a dependency-existence check, and review of the diff before each commit. (Sections 3, 5 and 7)
4. **Train calibration**: learners predict whether a change works before checking; show METR/Perry results. (Sections 1 and 5)
5. **Encourage "ask why" use over pure delegation**, especially early. A guard-railed tutor mode or instruction file can push the agent to explain. (Sections 1 and 2)
6. **Reduce setup friction**, for example a cloud environment or a setup clinic first, with local setup later using the agent. (Section 4)
7. **Assess judgment**: process log, short oral walkthrough of the capstone, and a rubric on specification, verification evidence, justified rejection of AI output, and Git hygiene. (Section 6)
