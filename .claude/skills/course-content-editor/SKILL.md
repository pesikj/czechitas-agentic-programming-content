---
name: course-content-editor
description: Write, update and restructure lecture materials for the Czechitas course "Programování s AI" (Python + Codex/Claude Code for beginners) in this content repository. Use this skill whenever the user wants to add or edit a lecture, part, exercise or example, shorten or simplify existing material, check that content matches the syllabus, add use cases, reorder or split lectures, or edit course.yaml / lecture.yaml — even if they just say "uprav lekci 3", "doplň příklad" or "tohle je moc složité". For review-only requests ("zkontroluj", "zrecenzuj") use course-content-reviewer instead.
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

When the user asks only for a review ("zkontroluj"), use the `course-content-reviewer` skill and don't edit anything.

## Lecture structure

Every lecture has these four sections, in this order. **Úvod is its own part file, `01-uvod.md`** (front matter `id: uvod`, `title: Úvod`), listed first in `lecture.yaml`, so the website shows it as a separate page before the content. The organizer wants learners to see the lecture's plan on its own page, not mixed into the first topic. **Obsah** follows in content parts, and a content part should be long: about **3–5 A4 pages** (roughly 1,500–3,000 words), structured with `##`/`###` headings. Don't split content into many short part files; start a new content part only when the current one would exceed about 5 pages. **Shrnutí and Kam dál are always two separate part files** at the end of the lecture, and you must update both every time the lecture content changes.

1. **Úvod** (introduction): every lecture starts with it, as the separate first part `01-uvod.md`. Its main heading is the lecture name without the number (for example `# Python v době AI`). It has three elements, in this order:
   - **What we will cover:** the topics of the lecture as a short numbered list, in the order they come, with one sentence each. Open with a sentence linking back to the previous lecture.
   - **Why (motivation):** why these topics are taught, and why now. Name the problem the learner will be able to solve, why it matters for their own app and for working with the agent, and how it builds on what they already know. Use 2–4 sentences.
   - **Competences:** 3–5 concrete skills the learner gains, phrased as "Umíš..." / "Víš, kdy...". This is the promise that Shrnutí fulfils, and every competence from the introduction must appear there.

   Keep the whole introduction to about half an A4 page, for example:

   ```markdown
   ---
   id: uvod
   title: Úvod
   ---

   # Název lekce

   Minule jsi ... Dnes na to navážeme:

   1. **Téma** – jedna věta, o čem to je.
   2. **Další téma** – ...

   **Proč to potřebuješ:** ...

   **Po lekci budeš umět:**
   - Umíš ...
   - Víš, kdy ...
   ```
2. **Obsah** (content): the concepts of the lecture, one after another, with each concept built as described below.
3. **Shrnutí** (conclusion): a summary of what we learned, as a list of **at most 5 bullets** with concrete skills ("Umíš...", "Víš, kdy..."), not topic names. The organizer wants learners to take away the few things that matter, not a checklist of every term. When the lecture teaches more, merge related skills into one bullet and leave out details.
4. **Kam dál** (next steps): **at most 5 bullets** with proposals for extending the knowledge, such as a small extra task for the learner's project, something to try with the agent, or a good resource. Keep the optional "Chceš vědět víc?" link line and one sentence previewing the next lecture below the bullets; they don't count toward the limit.

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

- **Syllabus fit.** The topic belongs to this lecture according to `references/syllabus.md`, and it doesn't jump ahead. For example, don't use Git in lecture 2 or deployment before lecture 10. If the user wants something that conflicts with the syllabus, make the change and point out the conflict.
- **Consistency.** Use the same term for the same thing throughout. Before introducing a new name, check how earlier lectures named it (`grep -ri` the repository).
- **Correctness.** Commands and code must actually work for a beginner on macOS and Windows. Don't invent CLI flags or tool features. If you aren't sure about current Codex or Claude Code behaviour, say so instead of guessing.
- **Downloadable files.** Store files that learners download (data such as CSV, sample code) in the lecture's `data/` folder and link them with a relative Markdown link from the part, e.g. `[nakup.csv](data/nakup.csv)`. Never link to the GitHub repository or `raw.githubusercontent.com`, and don't build download commands (`curl`) on repository URLs.
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
- [ ] The lecture has Úvod (separate part `01-uvod.md`) → Obsah → Shrnutí → Kam dál, and the intro and conclusion match the content
- [ ] Úvod lists the topics, explains why they are taught, and names the competences, and each competence appears in Shrnutí
- [ ] Shrnutí and Kam dál each have at most 5 bullets
- [ ] Each concept has a use case, a simple explanation and practical use (code, command or prompt)
- [ ] Transitions connect the concepts into one logical story
- [ ] Matches the syllabus and builds only on earlier lectures
- [ ] No paragraph or detail the learner doesn't need for this lecture
- [ ] Czech, *ty*, both genders in the "myslel(a)" bracket style, terms explained on first use
- [ ] Code, commands and prompts in the correct fenced blocks, and they work
- [ ] IDs are unchanged for existing parts and exercises, and new IDs are unique
- [ ] An exercise `revision` is increased only when its meaning changed
- [ ] Validator passes
