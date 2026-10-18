---
name: course-content-editor
description: Write, update, review and restructure lecture materials for the Czechitas course "Programování s AI" (Python + Codex/Claude Code for beginners) in this content repository. Use this skill whenever the user wants to add or edit a lecture, part, exercise or example, shorten or simplify existing material, check that content matches the syllabus, add use cases, reorder or split lectures, or edit course.yaml / lecture.yaml — even if they just say "uprav lekci 3", "doplň příklad", "zkontroluj obsah" or "tohle je moc složité".
---

# Course content editor

This repository holds the materials for **Programování s AI: od základů k vlastní aplikaci**, a Czechitas course for complete beginners. Learners write Python with an AI coding agent (Codex, optionally Claude Code). A separate website (`../czechitas-agentic-programming`) reads this repository and shows each lecture one part at a time, next to the learner's terminal and editor.

Every change should leave the content in three states:

1. **In check:** it matches the syllabus, stays consistent with the other lectures, and passes the validator.
2. **Concise:** it is short, plain and practical, without technical detail the learner doesn't need yet.
3. **Grounded:** each new concept comes with a short, concrete use case.

## Workflow

1. **Read before you write.** Before extending or changing a lecture, read the whole lecture: `lecture.yaml` and every part in order, not just the part you will touch. Also read `course.yaml`, skim the previous lecture's conclusion, and check the topic in `references/syllabus.md`. New text must continue what is already there: the same running example, the same terms, the same tone, and nothing explained twice. A lecture can rely only on concepts introduced before it.
2. **Write.** Write or change the content using the lecture structure and rules below and the format in `references/content-format.md`.
3. **Check.** Run the validator (see "Validation"), then review your edit against the checklist.
4. **Report.** Briefly tell the user what changed, any syllabus conflicts you noticed, and the validator result. Don't paste the whole lecture back.

When the user asks only for a review ("zkontroluj"), don't edit anything. List the problems by file and line, ordered by impact, and offer to fix them.

## Lecture structure

Every lecture has these four sections, in this order. **Úvod and Obsah go together into one content part file**, and a content part should be long: about **3–5 A4 pages** (roughly 1,500–3,000 words), structured with `##`/`###` headings. Don't split content into many short part files; start a new content part only when the current one would exceed about 5 pages. **Shrnutí and Kam dál are always two separate part files** at the end of the lecture, and you must update both every time the lecture content changes.

1. **Úvod** (introduction): a short summary of what the lecture covers and the motivation for it. Say what problem the learner will be able to solve by the end and why it matters for their own app. Link back to what they learned last time. Keep it to a few sentences.
2. **Obsah** (content): the concepts of the lecture, one after another, with each concept built as described below.
3. **Shrnutí** (conclusion): a summary of what we learned, as a short list of concrete skills ("Umíš...", "Víš, kdy..."), not a list of topic names.
4. **Kam dál** (next steps): proposals for extending the knowledge, such as a small extra task for the learner's project, something to try with the agent, or 1–3 good resources. Add one sentence previewing the next lecture.

When you extend an existing lecture, put new material in the content part and update the introduction, `Shrnutí` and `Kam dál` so they still describe the lecture accurately.

### Building one concept

Present each concept in the content section with these three elements, usually in this order:

1. **Practical use case and example:** a specific situation that shows the abstract concept on something concrete (see "Use cases" below).
2. **Simple explanation:** what the concept is, in plain Czech, with an analogy if it helps. Keep it to a few sentences.
3. **Practical use:** how to actually use it. Show a short piece of code, a terminal command, or a prompt for the agent, plus the expected output or a way to check that it worked.

An optional exercise can follow when the learner should try the concept themselves.

### Logical flow

All parts of the text should read as one connected story, not a collection of separate notes:
- Give each concept a sentence that connects it to the previous one ("Teď už umíš X. Co když ale...").
- Prefer a single running example that grows through the lecture (for example, the same small app) over a new unrelated example for each concept.
- The introduction promises what the conclusion summarises, and the conclusion leads into the next steps.
- When you add or move content, reread the neighbouring paragraphs and fix any transition the change broke.

## Writing rules

**Language and voice.** Write in Czech and address the learner informally with *ty*. Address both genders: where the learner's gender shows, write the masculine form with the feminine ending in brackets, for example "myslel(a)", "zvládl(a) jsi", "sám(a)", "jistý(á)". Never write only the feminine or only the masculine form. Words that refer to something else, such as "AI sama píše" or "práce vypadala", keep their normal form. Keep established English terms the learner will meet in tools (commit, prompt, repository, traceback, MCP) and explain each one in one short sentence the first time it appears.

**Terminology.** Say "programová logika", never "programátorská logika" (the organizer considers it offensive).

**Quotation marks.** Always use straight double quotes `"..."`. Never use Czech typographic quotes `„` and `“` (or `”`), not even in Czech prose.

**Ellipsis.** Always write three normal dots `...`. Never use the single ellipsis character `…`.

**Concise means:**
- One idea per paragraph, and paragraphs of at most about 4 sentences.
- Keep sentences and paragraphs short, but not the part: a content part is about 3–5 A4 pages. Use headings so the learner can navigate it.
- Explain *what it is*, *why it matters*, and *how to use it*. Leave out internals, history, edge cases and alternatives unless the lecture is about them.
- If a detail is true but not needed for today's task, cut it. If it might help some learners, add one link to the "Chceš vědět víc?" line at the end.
- Avoid jargon chains ("tokenizace kontextového okna LLM"). Replace them with an analogy or a concrete effect ("agent si pamatuje jen omezené množství textu — dlouhá konverzace ho začne mást").

**Use cases.** Introduce each concept with a short practical situation of 1–3 sentences, close to the learner's own project. Use this form:

```markdown
> **Kdy se to hodí:** Píšeš aplikaci na evidenci knih a chceš vyzkoušet, jestli by agent zvládl přidat hledání. Nejdřív si uděláš commit — když se pokus nepovede, vrátíš se jedním příkazem zpět.
```

Good use cases are concrete (real file names, real numbers), reachable at the learner's current level, and show *why* the concept matters, not just that it exists. Make most of them about Python apps and work with the agent, not abstract computer-science examples.

**AI framing.** The course message is "AI is a partner, but you understand what is being built." Exercises should make the learner read, explain, verify or change what the agent produced, not just accept it. Where it fits, follow the workflow **explore → plan → code → test → commit**.

**Code and prompts.** Keep code examples short (ideally under 15 lines) and runnable as shown. Separate the different kinds of input clearly:
- terminal commands in ` ```bash `
- Python in ` ```python `
- prompts for the agent in ` ```text `, introduced by a line like "Prompt pro agenta:"
- expected output in ` ```text `, introduced by "Výstup:"

**Tool differences.** Codex is the primary tool. When steps differ between Codex and Claude Code, or between macOS and Windows, use an `::::alternatives` block rather than writing both into the prose.

## Keeping content "in check"

- **Syllabus fit.** The topic belongs to this lecture according to `references/syllabus.md`, and it doesn't jump ahead. For example, don't use functions in lecture 2 or Git in lecture 3. If the user wants something that conflicts with the syllabus, make the change and point out the conflict.
- **Consistency.** Use the same term for the same thing throughout. Before introducing a new name, check how earlier lectures named it (`grep -ri` the repository).
- **Correctness.** Commands and code must actually work for a beginner on macOS and Windows. Don't invent CLI flags or tool features. If you aren't sure about current Codex or Claude Code behaviour, say so instead of guessing.
- **Safety.** Never put real API keys, passwords or personal data in examples. Use obvious placeholders such as `TVUJ_API_KLIC`.
- **Exercises.** Keep them optional and short, with a clear result the learner can verify.

## Validation

The website project includes a content validator. Run it from the content repository:

```bash
cd ../czechitas-agentic-programming && npm run content:validate -- ../czechitas-agentic-programming-content
```

Fix every `ERROR` (an error blocks publishing). Fix warnings unless there's a reason not to, such as a screenshot that hasn't been added yet. In that case, mention it to the user. If the validator can't run (for example, dependencies aren't installed), say so and check the rules in `references/content-format.md` by hand.

## Final checklist

- [ ] The whole lecture was read before editing, and the new text fits it
- [ ] The lecture has Úvod → Obsah → Shrnutí → Kam dál, and the intro and conclusion match the content
- [ ] Each concept has a use case, a simple explanation and practical use (code, command or prompt)
- [ ] Transitions connect the concepts into one logical story
- [ ] Matches the syllabus and builds only on earlier lectures
- [ ] No paragraph or detail the learner doesn't need for this lecture
- [ ] Czech, *ty*, both genders in the "myslel(a)" bracket style, terms explained on first use
- [ ] Code, commands and prompts in the correct fenced blocks, and they work
- [ ] IDs are unchanged for existing parts and exercises, and new IDs are unique
- [ ] An exercise `revision` is increased only when its meaning changed
- [ ] Validator passes
