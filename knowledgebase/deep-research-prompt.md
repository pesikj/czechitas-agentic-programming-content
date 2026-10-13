# Deep research prompt: competitive course benchmarking

Research the best available online courses in **agentic coding and AI-assisted software development**, and recommend how to make our Czechitas course competitive in topic coverage, teaching quality, and practical learning outcomes.

### Our course

We are designing a course with these constraints:

- **10 lectures, each approximately 2.5–3 hours**: 25–30 teaching hours in total.
- Learners understand general AI concepts and are experienced users of ChatGPT.
- **No prior programming, Git, GitHub, VS Code, or coding-agent experience is required.**
- Most learners are expected to use Windows/PowerShell; others will use macOS or Linux.
- The goal is to help learners direct coding agents, understand generated code, evaluate changes, test applications, and deploy working software.
- We teach Python literacy so learners can reason about generated code. Becoming proficient at writing code from scratch is not the primary objective.
- Teaching combines explanations, guided exercises, and increasingly independent practical work.
- Deployment exercises should use free services or free trials. The budget for coding-agent subscriptions is not yet decided.

Our current **provisional outline** is:

1. Python code literacy, VS Code, environment setup, and first use of a coding agent.
2. Functions, exceptions, and understanding execution through the debugger.
3. Git and GitHub for change review, checkpoints, and rollback.
4. Shell literacy and operating coding agents: prompts, permissions, models, usage, and observing actions.
5. Agentic development workflow: explore, plan, implement, verify, review, and commit, using a small existing Django application with SQLite locally.
6. Testing and validation: unit and integration tests, investigating failures, and recognizing that passing tests can still validate the wrong requirement.
7. Getting an unfamiliar FastAPI/React repository running, making a feature change or bug fix, and introducing end-to-end verification.
8. Deployment, primarily of the Django application.
9. Advanced agent usage: context, memory, repository instructions, skills, MCP, and sub-agents.
10. A practical capstone that combines implementation, testing, and deployment.

This outline is open to revision. **Evaluate it critically rather than assuming its structure or technology choices are correct.**

### Research objectives

Identify what excellent comparable courses teach, how they teach it, and what evidence supports their quality. Recommend a realistic curriculum that matches or exceeds the strongest relevant offerings **for our specific beginner audience**.

Distinguish:

- Direct competitors aimed at non-programmers or beginners.
- Adjacent courses for experienced developers that provide useful teaching ideas.
- Official vendor tutorials and documentation that establish technical coverage but are not complete courses.

Do not treat popularity, search ranking, affiliate recommendations, or marketing claims as sufficient evidence of quality.

### Research method

1. Find approximately **10–15 relevant offerings**, then examine the **5–8 strongest or most comparable** in depth. Prefer fewer well-documented courses over a padded list.
2. Include a mix of independent educators, established learning platforms, and official training from relevant tool providers.
3. Search across terminology such as *agentic coding*, *AI-assisted development*, *AI coding agents*, *vibe coding*, *Claude Code*, *Codex*, *Cursor*, and *GitHub Copilot*.
4. Focus on learning to develop software with coding agents. Separate this from courses primarily about building LLM applications or agent frameworks.
5. Prioritize current curricula and identify their publication or last-update dates where available.
6. Use primary sources: official course pages, detailed syllabi, sample lessons, public exercise repositories, assessment descriptions, and instructor materials. Supplement these with credible independent reviews where useful.
7. Do not infer course coverage from its title. Mark information as **verified**, **inferred**, or **not publicly available**.
8. Cite direct links for factual comparisons and recommendations. Record the research date and verify current prices and access conditions.
9. If lessons or assessments are behind a paywall, state the limitation. Do not claim to have assessed their teaching quality from a landing page alone.

### Questions to investigate

**Topic coverage**

Which topics recur in the strongest comparable courses? Which are essential, optional, advanced, or mainly vendor-specific?

Investigate at least:

- Programming literacy and reading unfamiliar code.
- Environment setup, terminal use, and dependency management.
- Breaking a task into requirements and acceptance criteria.
- Giving agents useful context and writing effective task instructions.
- Repository exploration, planning, implementation, and iteration.
- Git, reviewing diffs, rollback, and collaboration.
- Debugging and responding to agent failures.
- Unit, integration, and end-to-end testing.
- Verifying outcomes independently of the agent’s own tests.
- Context management, persistent instructions, memory, and reusable skills.
- MCP and external tools.
- Sub-agents and parallel work.
- Permissions, secrets, prompt injection, and dependency risks.
- Frontend/backend/database concepts.
- Deployment, configuration, logs, and basic maintenance.
- Model selection, cost management, and tool limitations.
- Knowing when to intervene, restart, simplify, or seek human help.

Also identify valuable topics absent from this list.

**Teaching quality**

How do strong courses handle:

- Beginners’ cognitive load and setup problems?
- The transition from following demonstrations to independent problem solving?
- Realistic projects and existing codebases?
- Deliberately flawed outputs, failed tests, and recovery exercises?
- Feedback, assessments, rubrics, and capstones?
- Transferable skills across tools rather than memorizing interfaces?
- Rapid tool changes and maintenance of course materials?

**Fit and differentiation**

- Is our proposed scope realistic in 25–30 hours?
- Are two early Python-focused lectures appropriate, or should code literacy be integrated throughout?
- Does using Django plus FastAPI/React add useful transfer practice or excessive complexity?
- Which advanced topics deserve hands-on practice versus a short demonstration?
- What should we remove or shorten to make room for missing essentials?
- How can the course stand out through demonstrable learning outcomes rather than a longer topic list?

### Required deliverables

1. **Executive recommendation:** the most consequential changes, their rationale, and the strength of supporting evidence.
2. **Competitor comparison table:** provider, course, intended audience, prerequisites, duration, tools, projects, assessments, price/access, update date, and sources. Explain why each offering was selected.
3. **Topic coverage matrix:** compare our proposed course with the strongest relevant offerings. Distinguish a topic being mentioned from demonstrated practice or assessed mastery.
4. **Prioritized gap analysis:** classify recommendations as:
   - Essential.
   - Valuable if time permits.
   - Optional follow-up material.
   - Unsuitable for this audience or time budget.

   For every addition, explain what should be shortened, replaced, or removed.
5. **Revised 10-lecture syllabus:** provide each lecture’s learning outcomes, prerequisites, key topics, practical exercise, observable evidence of learning, and approximate timing. Design a **150-minute core with an optional 30-minute extension** per lecture.
6. **Assessment plan:** propose lightweight progress checks and a capstone rubric that assesses learner judgment and the resulting application, not merely whether the agent produced code.
7. **Three to five credible differentiators:** explain how we could provide a better learning experience for beginners and how each advantage could be demonstrated.
8. **Delivery and maintenance considerations:** Windows/macOS/Linux support, learner costs, setup preparation, and which materials require frequent updates.
9. **Open decisions and evidence limitations:** clearly separate research-backed conclusions from your curriculum-design judgment.

Keep the recommendations practical. Our aim is **strong learning outcomes within a fixed beginner course**, not exhaustive coverage of every tool or trend. Summarize curriculum ideas in your own words; do not reproduce proprietary teaching materials.
