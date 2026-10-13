# Syllabus: Programování s AI: od základů k vlastní aplikaci

Source: the course outline Google Doc "osnova_python_ai". If the user says the syllabus has changed, update this file.

**Audience:** complete beginners with no programming experience. They need a paid ChatGPT Plus plan (Codex); Claude Pro (Claude Code) is an alternative that works slightly differently.

**Core message:** AI won't think for you. You use it as a partner that helps design, explain, write, test and fix code, while you understand what is being built and why.

**Final project:** your own simple Python app, going through **nápad → specifikace → plán → Python → testování → debugging → Git → spuštění**. The learner should be able to explain how it works and keep changing it on their own.

## Lectures

| # | Topic | What the learner actually learns | Not yet / limits |
|---|---|---|---|
| 1 | Python v době AI + první program | What development with AI looks like today, Codex vs. regular chat, VS Code, terminal, running Python, first script. Variables, data types, `print()`, `input()`. The difference between "AI built something" and "I understand what it built" | No conditions, loops or functions |
| 2 | Podmínky a práce s daty | `if/elif/else`, operators, strings, numbers, lists. Reading and changing existing code. First small tasks with Codex: explain → propose a change → change → verify | No functions, no Git |
| 3 | Cykly, funkce a struktura programu | `for`, `while`, functions, parameters, return values. Breaking a problem into smaller parts. Knowing where to change AI-generated code | No Git yet |
| 4 | Terminál, Git a GitHub | Files and directories, terminal commands, `pip`, dependencies. Git: repository, status, add, commit, diff, history. GitHub. Markdown/README. Why version control matters when working with an agent | |
| 5 | Codex: od promptování k agentnímu vývoji | What a coding agent is, the context window, instructions, permissions. **explore → plan → code → test → commit**. Let the agent understand the project first instead of generating code right away | |
| 6 | Návrh vlastní aplikace s AI | Product thinking, kept light: problem, user, inputs/outputs, MVP, Definition of Done. Breaking the app into features. Making a plan with the agent. Start of the final project | |
| 7 | Debugging a testování s AI | Error messages, traceback, `print()` debugging, finding the cause instead of rewriting code at random. Basic automated tests. Checking that an AI fix didn't break something else | |
| 8 | Kontext, bezpečnost, pokročilá práce s agentem | Managing context on a longer project, memory/instructions, permissions, secrets and sensitive data. Security of AI-written code. **Skills and MCP only as a practical taste** | No deep dive into Skills or MCP |
| 9 | Od Python kódu k aplikaci | Finishing the project, packages, dependencies, configuration. What deployment means. Docker only as far as deployment needs it. Deployment and fixing problems after it | Docker only to the extent it is needed |
| 10 | Project lab: dokončení, audit, prezentace | Independent work with mentor support. Tests, code review with the agent, a basic security check, README, final commit. Presentation and reflection: what the AI wrote vs. what I understand | |

## Course-level learning outcomes

Python basics (variables, types, conditions, loops, functions) · breaking a problem down · reading and changing simple code · terminal and dev environment · Git/GitHub · Codex for planning, writing, changing and reviewing code · context and instructions for the agent · testing and debugging, including AI-written code · basic security risks · building, finishing and running your own app.
