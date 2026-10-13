# Course memory

Last updated: 2026-10-07.

Source: [Agentic Coding Brainstorming](agentic-coding-brainstorming.md), exported from the [shared conversation](https://chatgpt.com/share/6ac63eba-fa6c-83ed-a88a-3921231acd3f). This file records course context from that discussion; it is not a finalized syllabus.

## Organization

- **Subject:** agentic coding — using AI coding agents to build, modify, test, and deploy software.
- **Number of lectures:** **10**. The organizer explicitly corrected the initial statement of eight lectures to ten (transcript message 28).
- **Lecture duration:** **2.5–3 hours**, with the exact duration still undecided (message 7).
- **Total teaching time:** approximately **25–30 hours**, calculated from the planned lecture count and duration.
- **Format:** a combination of explanations and practical work. Some lectures focus on projects; not every lecture must advance one shared project.
- **Deployment cost constraint:** learners should be able to use a free service or a free trial without an additional deployment charge (message 72).

## Audience and prerequisites

- Learners are expected to understand general AI concepts and be advanced users of tools such as ChatGPT.
- No prior programming experience is required.
- No prior experience with coding agents such as Claude Code, Codex, or Cursor is required.
- No prior Git, GitHub, or Visual Studio Code experience is assumed.
- The organizer expects most learners to use Windows/PowerShell, with a minority using macOS or Linux. Teaching materials should accommodate these environments; this is an expectation, not a confirmed enrollment breakdown.

## Learning goals and teaching approach

- Enable learners to direct coding agents and understand, review, and validate their work.
- Teach enough Python to recognize and reason about generated code, including conditions, loops, functions, and exceptions. Writing code from scratch is not the central goal.
- Use the debugger to make execution flow visible.
- Teach Git as a way to inspect changes, preserve working versions, and roll back unwanted changes.
- Practice planning, implementation, running applications locally, testing, reviewing changes, and committing.
- Have learners run tests, see failures, and use AI to investigate them. Emphasize that passing tests does not guarantee the implementation meets the original requirement.
- Include practical work with existing applications: adding features, fixing bugs, setting up unfamiliar repositories, and deploying software.
- Show that agents can help with setup and other supporting tasks as well as writing code, and that the workflow transfers across technologies.

## Technology direction discussed

- Subsequently confirmed by the organizer: preparatory lecture 00 is a concise installation guide in Czech, with separate pages for Windows and macOS. Required software: uv, Python installed through uv immediately after uv installation, Visual Studio Code, and Git; additionally Homebrew on macOS. Include Docker Desktop with a note that it is needed later in the course, and a GitHub account registration step. See `lectures/00-instalace/`.
- Python is the main language, with Visual Studio Code and coding agents introduced early.
- Learners install both the desktop application and CLI for either Codex or Claude Code, choosing the product covered by their subscription. Use Homebrew for these installations on macOS. Both products are alternatives; installing both is not required.
- A small Django application with SQLite for local work was accepted as the main workflow example.
- FastAPI with a React frontend was discussed as a contrasting application architecture.
- Deployment should be included, primarily using the Django application. Render was suggested by the assistant; the provider was not explicitly finalized. Pricing and free-tier claims in the transcript are historical suggestions, not verified course requirements.
- The organizer requested advanced agent usage, including skills and memory. The assistant proposed instruction files, MCP, and sub-agents, followed by a capstone; the final lecture allocation remains a proposal.

## Not yet established

Repository status: the organizer requested removal of placeholder lectures 01–03. Only preparatory lecture 00 remains in the course navigation; this does not change the planned ten-lecture course scope.

- Exact session duration, dates, frequency, and delivery mode (online or in person).
- Enrollment size, instructors, homework expectations, assessment, or certification.
- Course teaching language: the request to speak English concerned the brainstorming conversation, not necessarily the course.
- Specific subscription tiers and learner budget for AI tools; the product choice follows the learner's existing subscription (Codex or Claude Code).
- Final syllabus, deployment provider, and capstone specification.
