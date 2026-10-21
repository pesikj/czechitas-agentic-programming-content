# Content format (contract with the course website)

The website `../czechitas-agentic-programming` loads this repository (`src/lib/content/load.ts`). Breaking these rules blocks publishing.

## Structure

```
course.yaml
lectures/
  01-python-a-ai/
    lecture.yaml
    01-uvod.md
    02-python-a-ai.md
    03-shrnuti.md
    04-kam-dal.md
    images/
      vscode-terminal.png
```

### course.yaml

```yaml
title: Programování s AI
toc:
  - title: Základy Pythonu        # optional group, needs items
    items:
      - lecture: 01-python-a-ai   # directory name inside lectures/
      - lecture: 02-podminky
  - lecture: 03-funkce
```

A lecture directory that isn't listed in the `toc` won't be shown (warning).

### lecture.yaml

```yaml
id: python-a-ai
title: Python v době AI + první program
parts:            # order = order shown to learners
  - 01-uvod.md            # Úvod: a separate page with topics, motivation and competences
  - 02-python-a-ai.md     # Obsah: one content part of about 3–5 A4 pages
  - 03-shrnuti.md         # Shrnutí: what we learned, updated with every content change
  - 04-kam-dal.md         # Kam dál: next steps, updated with every content change
```

A `.md` file in the directory that isn't listed in `parts` won't be shown (warning).

Optional `public: true` (next to `title`) makes the lecture and its images readable without signing in, and the sign-in page links to it. Use it only for material learners need before the course, such as tool installation; everything else stays sign-in only.

### Part file

Part files are numbered from `01` in the order they are shown (`01-uvod.md`, `02-...`), confirmed by the organizer on 2026-10-18.

Each part must start with front matter that contains only `id` and `title`:

```markdown
---
id: prvni-program
title: První program
---

Text...
```

## IDs

- Use the pattern `^[a-z0-9]+(-[a-z0-9]+)*$`: lowercase ASCII, digits and hyphens. No diacritics.
- Lecture IDs are unique in the course, part IDs are unique within their lecture, and exercise IDs are unique in **the whole course**.
- **Never rename an existing ID.** Saved learner answers and bookmarks depend on it. To move or rename content, change the file name, title or order and keep the ID.

## Exercises

An exercise is a fenced block with the language `exercise`. It contains YAML:

````markdown
```exercise
id: vysvetli-kod
revision: 1
title: Nech si vysvětlit kód
fields:
  - id: prompt
    label: Použitý prompt
  - id: vysledek
    label: Výsledek a ověření
    guidance: Co agent vysvětlil a jak jsi ověřila, že má pravdu?
  - id: reflexe
    label: Reflexe
```
````

- Allowed keys: `id`, `revision` (a positive integer), `title` (optional), and `fields` (at least one).
- Each field has `id`, `label` and an optional `guidance`. Field IDs are unique within the exercise.
- Increase `revision` only when the task meaningfully changes. The website then marks older answers as belonging to a previous version.
- Write the task instructions as normal Markdown above the block.

## Alternatives (OS or tool variants)

```markdown
::::alternatives
:::option{label="Codex"}
Spusť `codex` v terminálu.
:::
:::option{label="Claude Code"}
Spusť `claude` v terminálu.
:::
::::
```

Use at least two options, and give each one a `label`. Any other directive is shown as plain text (warning).

## Images

- Use standard Markdown `![alt text](images/file.png)` with a path **relative to the .md file**, stored inside the repository.
- Allowed file types: png, jpg, jpeg, gif, webp, svg. Paths are case-sensitive.
- Alt text is required (warning). Describe what the image shows, in Czech.
- External image URLs aren't protected by sign-in (warning). Store a copy in the repository instead.

## Downloadable files

Files for learners to download (CSV data, sample code) live in the lecture's `data/` folder and are linked with a relative Markdown link, for example `[nakup.csv](data/nakup.csv)`. Don't link to the GitHub repository.

Note (2026-10-18): the website currently serves only images (`src/pages/obsah/[...path].ts` serves an allowlist of image assets), so relative links to other files don't work there until the website adds support for downloads.

## Markdown

Use CommonMark + GFM: tables, task lists, strikethrough and autolinks. Raw HTML isn't rendered (warning), so use Markdown only.
