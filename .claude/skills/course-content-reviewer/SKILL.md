---
name: course-content-reviewer
description: Review a lecture (or one part of it) of the Czechitas course "Programování s AI" in this content repository and report problems without editing anything. Checks logical coherence, missing topics/explanations/examples, prerequisites that earlier lectures never taught, whether Shrnutí and Kam dál match the content, and whether examples, code, outputs and exercises are correct and realistic for complete beginners, and whether the lecture with its exercises fits a 3-hour session (not too long, not too short). Use this skill whenever the user asks to review, check, proofread, audit or give feedback on lecture material, even if they just say "zkontroluj lekci 1", "zrecenzuj to", "projdi 04-chyby-a-balicky.md", "dává to smysl?", "pochopí to účastníci?", "je shrnutí aktuální?", "není to moc dlouhé?" or "stihneme to za 3 hodiny?".
---

# Course content reviewer

You review lecture materials for **Programování s AI**, a Czechitas course for complete beginners who write Python with an AI coding agent (Codex, optionally Claude Code). Your job is to find what would confuse, mislead or block a learner, and to report it so the organizer can fix it (usually with the `course-content-editor` skill).

**You don't edit files.** The output is a report. If the user then asks you to fix something, that's a separate step and the editor skill's rules apply.

## Who you're reviewing for

Read every text as one specific learner would: an adult who is an advanced ChatGPT user, has **never programmed**, has never used a terminal, Git or VS Code before this course, most likely sits at **Windows with PowerShell**, and has nothing but this lecture, the previous lectures and lecture 01 (installation). They can't ask the author what was meant. Most problems worth reporting are moments where this person would stop and think "what? how? where did that come from?".

The course goal also matters: learners should *understand and verify* what the agent builds, not write code from scratch. An example that requires writing code alone is a level problem. An example that only says "let the agent do it" without the learner checking anything misses the course message.

## Gather context first

A review is only as good as the context behind it. Before writing any finding, read:

1. `knowledgebase/course-memory.md` (paths here are relative to the repository root). It has the audience and the **confirmed organizer decisions**, including deliberate deviations from the syllabus. A deviation that the memory records as the organizer's choice is not a defect. Mention it at most once as context, not as a finding.
2. The syllabus: `.claude/skills/course-content-editor/references/syllabus.md`. Find the row for the reviewed lecture and the rows after it, so you know what is *supposed* to come later.
3. `course.yaml` and the lecture's `lecture.yaml`, to get the part order the learner actually sees.
4. **The whole reviewed lecture**, every part in `parts` order, even when only one part is under review. Coherence and Shrnutí problems are invisible from a single file.
5. **All earlier lectures** in `course.yaml` order, including lecture 01 (installation). For long ones, read headings, every place a new term is introduced (italic `*term*` definitions, "Kdy se to hodí" blocks) and the exercises. Don't trust their Shrnutí alone: it can claim things the content never taught.
6. The first part of the **next lecture**, if it exists, to check the Kam dál preview.

Use `grep -rn` across `lectures/` to answer "was X explained before?" quickly, and `cat -n` so you can cite line numbers.

## What to check

Work through these six areas. For each one, the questions below are the core. Use judgment about what else belongs under them.

### 1. Logical coherence

- Does the lecture read as one story? The intro promises something, the content delivers it in a sensible order, and each concept connects to the previous one.
- Is every term used only after it's explained? Search for the first occurrence of each new term and compare it with where it's defined.
- Are back-references true? "Jak jsme spočítali v trasovací tabulce", "projekt, který sis vytvořil(a) minule", "stejně jako u eur" each point to something. Find it, and check that it really is there and says the same thing (same numbers, same file names, same folder).
- Do parts contradict each other? Look at file and folder names, numbers, commands and how a tool is described.
- Is the running example consistent: same data, same file names, same variable names across parts?

### 2. Gaps

Report a gap only when a learner would actually get stuck or misunderstand. Don't report it just because more could be said. The course deliberately stays concise.

- **Missing step:** an instruction the learner can't carry out with what they've been told. Where do I save it? Which folder is the terminal in? How do I open this? What do I do on Windows?
- **Missing explanation:** a term, symbol or piece of syntax shown in code or output that the learner needs to understand, but nobody explains.
- **Missing example or check:** a concept explained only abstractly, or a task with no expected output or other way to verify that it worked.
- **Missing syllabus topic:** something the syllabus row lists for this lecture that is not covered and isn't recorded as postponed in the course memory.
- **Missing platform variant:** a step that differs on Windows and macOS (paths, commands, shortcuts) but is described for only one.

### 3. Prerequisites

List every concept, command, tool or skill the lecture **assumes** without explaining it. For each one, find where it was taught: earlier in this lecture, an earlier lecture, or lecture 01 (installation).

- Not taught anywhere → a finding. Say whether it should be explained here or whether the syllabus places it in a later lecture.
- Taught only in a *later* lecture according to the syllabus, but used here as if known → a finding, unless the course memory records it as a deliberate choice.
- Assumed from lecture 01 (installation): check that the installation guide really installs it on **both** Windows and macOS.

### 4. Shrnutí and Kam dál

These parts are supposed to be updated with every content change, so they drift easily. Compare them line by line:

- **Every Shrnutí bullet is backed by the content.** Check the details: "Umíš X v terminálu" is wrong if the content did X in a browser.
- **Every major concept of the content appears in Shrnutí.** List the content's concepts (roughly one per `##` section) and tick them off.
- Shrnutí bullets are concrete skills ("Umíš...", "Víš, kdy..."), not topic names.
- **Every Kam dál task is doable** with what the learner knows at the end of this lecture, and it's clear what result to aim for.
- The **preview of the next lecture** matches the next lecture's real content, or the syllabus if it doesn't exist yet. It also must not promise something the learner already did in this lecture.

### 5. Examples, code and exercises

Verify instead of trusting. An example with a wrong number teaches the learner to distrust the material, or worse, themselves.

- **Run the code.** Copy Python snippets and the lecture's `data/` files into a scratch directory outside the repository and run them (`python3` or `uv run`). Compare the real output with the "Výstup:" block. For "broken" variants (a syntax error, bad data), reproduce the break and check the error message.
- **Recompute numbers by hand** when the code can't run as shown: totals, conversions, numbers in prose.
- **Check details inside outputs:** line numbers in a traceback should match the code as shown, and file names and paths should match what the learner created.
- **Commands:** would they work in PowerShell *and* in zsh? Watch for `ls -la`, `cat`, `~`, `/` vs `\`, `&&`, and quoting. Don't invent tool behaviour. If you aren't sure how Codex or Claude Code behaves now, say so instead of claiming an error.
- **Agent prompts:** are they realistic? Would an agent given this prompt plausibly produce what the text claims? Does the text prepare the learner for a different result ("tvůj kód se může lišit")?
- **Learner level:** can the learner understand the example with what they know at this point? Can they finish the exercise, and do they know when they're done? Does the exercise make them read, explain or verify, not just accept? Do the exercise `fields` match what the task asks for?

### 6. Length for one lecture session

A lecture is taught in one session of **3 hours** (the course memory records 2.5–3 h; review against 3 h unless the memory now says otherwise). Material that doesn't fit gets rushed or skipped, and the parts cut on the spot are usually the exercises, which is where learners actually learn. Material that is too thin wastes the session. Estimate whether the whole lecture fits, even when only one part is under review: say what share of the session that part takes.

Estimate it the way the lecture will actually run, for beginners in a classroom, not for a fast reader:

1. **Count** the words of each content part (`wc -w`, without Shrnutí and Kam dál), and per `##` section where a section looks heavy.
2. **Explanation:** about **8–12 minutes per 1,000 words** of prose and code the lecturer walks through, including questions. Tables, code walkthroughs and new terms are on the slow end.
3. **Hands-on steps:** every step the learners do themselves (open a project, download a file, run a command, run the agent and wait for it, break and fix something) costs about **5–10 minutes** for beginners, more on the first agent run and wherever Windows and macOS differ. Count them, don't guess them.
4. **Exercises** (`exercise` blocks): about **15–30 minutes** each including a short debrief, depending on how many steps and `fields` they have.
5. **Overhead:** subtract about **20–30 minutes** for the start, a break and wrap-up, which leaves roughly **150 minutes** of teaching time.
6. **Kam dál** is homework: don't count it, but note if it is so heavy that it reads like unfinished lecture content.

Give the estimate as a range, not a single number, and say which sections drive it. Then judge:

- **Too long** (the estimate's lower bound exceeds the teaching time): a finding. Severity is high when it is clearly over (more than about 20 %), otherwise medium. Suggest concretely what to cut, shorten or move, preferring topics the syllabus places in a later lecture and that the course memory doesn't record as a deliberate choice for this lecture. Never suggest cutting the exercises first.
- **Too short** (the upper bound is well under the teaching time, e.g. under ~110 minutes): a finding. Suggest which syllabus topic for this lecture, worked example or exercise would fill it.
- **Unbalanced:** e.g. 90 minutes of explanation before the first hands-on step, or no exercise in a long part. Report it as medium if learners would sit passively for a long stretch.

These rates are rough. Say that the estimate is rough, and don't report a length finding when the lecture is within the range.

### Also note, briefly

Mechanical rules from the editor skill: straight quotes `"..."` and three dots `...` (never `„“` or `…`), both genders in the "myslel(a)" style, "programová logika" (never "programátorská"), fenced block languages, and relative links to `data/`. Group all of these into **one** low-severity finding with the list of lines, so they don't drown out the real problems.

If the website repository is next door, you can also run the validator and include its errors:
`cd ../czechitas-agentic-programming && npm run content:validate -- ../czechitas-agentic-programming-content`

## Judging severity

- **High:** the learner gets stuck, gets a wrong result, or learns something false. Examples: wrong expected output, a command that fails on Windows, a concept used before it's ever taught, a Shrnutí claim the content contradicts.
- **Medium:** the learner can continue but will likely be confused, or the material no longer fits together. Examples: a broken back-reference, a missing Shrnutí entry, an unexplained symbol in code, a Kam dál task above their level.
- **Low:** polish, such as a weak transition, a style rule or a slightly better example.

Prefer fewer, well-supported findings over a long list of nitpicks. If you're unsure whether something is a problem, say so and explain what you'd need to check.

## Report

Write the report in the language the user wrote in. Quote lecture text in its original Czech. Use this structure:

```markdown
# Review: <lecture title> (<lecture dir>)

**Verdict:** <1–2 sentences: is it ready for learners, and what is the most important thing to fix?>

## Findings

### High
1. **<short title>** — `lectures/<dir>/<file>.md:<line>` · <category>
   - **Problem:** <what is wrong, with a short quote>
   - **Why it matters:** <what the learner will experience>
   - **Suggestion:** <concrete fix, 1–2 sentences>

### Medium
...

### Low
...

## Prerequisites check
| Assumed concept | Where it's used | Where it was taught |
|---|---|---|
<only list concepts that are interesting: missing, taught later, or borderline. Don't list every word>

## Length
| Part / section | Words | Hands-on steps | Exercises | Estimate (min) |
|---|---|---|---|---|
<one row per content part, heavy sections as extra rows, then a total row>

<1–2 sentences: does it fit a 3-hour session, what drives the length, what to cut or add>

## Shrnutí and Kam dál
<mismatches only: content not in Shrnutí, Shrnutí not backed by content, Kam dál problems, next-lecture preview>

## Verified
<one short list of what you actually checked and that was fine: which code you ran, which numbers matched. This tells the organizer what they don't need to recheck>
```

Categories: `coherence`, `gap`, `prerequisite`, `shrnuti-kam-dal`, `example`, `length`, `style`.

Leave out empty severity sections. End by offering to fix selected findings.
