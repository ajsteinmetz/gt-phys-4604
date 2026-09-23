# Course Conventions

Quarto website for a Georgia Tech physics course, instructor Andrew J. Steinmetz. Two sibling repos share one scaffold and one set of conventions: `gt-gt-1000` (GT 1000, First-Year Seminar) and `gt-phys-4604` (PHYS 4604, Professional Development). The shared conventions below are identical in both repos' `CLAUDE.md`; keep them in sync when either changes.

## Working in this repo

- When the user reports an error, explain the cause and the proposed fix first, then wait for a go-ahead before editing, especially for edits across many files.
- Preview with `quarto preview` (`.claude/launch.json` defines `quarto-preview` on port 4321 where present). Render a single file with `quarto render path/to/file.qmd`.
- `freeze: auto` is on. Rendered output of Python cells is committed under `_freeze/`, so a render normally needs no Python. Editing a file with Python cells re-executes them (needs matplotlib and numpy).
- Publishing is `quarto publish gh-pages`. Never edit the `gh-pages` branch, `_site/`, or `_freeze/` by hand.
- Semester rollover: tag the repo (e.g. `fall-2026`), then update semester, CRN, meeting time, and dates in `index.qmd`, `course-files/syllabus.qmd`, and the LaTeX syllabus.

## Characters and punctuation (ASCII-only source)

All `.qmd`, `.md`, and `.yml` source is ASCII-only. Write special characters as HTML entities:

| Character | Write | Use |
|---|---|---|
| Middle dot | `&middot;` | The separator: subtitles, footers, bold info lines, table cells (not `&bull;`) |
| Em dash | `&mdash;` | Parenthetical dash; list "item &mdash; description" |
| En dash | `&ndash;` | Ranges: `12:30&ndash;1:20 PM`, `September 14&ndash;15`, `2020&ndash;21` |
| Arrow, >=, <=, times | `&rarr;` `&ge;` `&le;` `&times;` | Prerequisite chains, thresholds |
| Accented letters | `&eacute;` `&ouml;` ... | Proper names (`Polit&eacute;cnica`, `Malm&ouml;`) |
| Copyright, degree, ellipsis | `&copy;` `&deg;` `&hellip;` | As needed |

- Do not use literal Unicode, `--`/`---` smart dashes, or `$\cdot$`-style math for punctuation. Reserve `$...$` for real equations.
- Spell **resume** without accents (Resume, resumes), never the accented form.
- Inside executable code chunks (Python), entities do not render; use `\uXXXX` escapes in string literals (backslash, `u`, then the 4-digit hex code: `u2013` for an en dash, `u2014` for an em dash).
- Escape a literal `@` in prose as `\@` (e.g. `Physics\@Tech`) so Pandoc does not read it as a citation.
- YAML front-matter strings use **double quotes**. Never put a backslash inside them (`"\cdot"` is an invalid YAML escape and breaks the build); entities avoid the need. If a value truly needs math or mixed quotes, use a folded block (`subtitle: >-` with the text indented on the next line).

## Language and voice

- Address students as **you**; the instructor writes as **I**/**we** ("We covered this in Lecture 1"). Direct, plain, warm; short sentences; no filler.
- Submission checklists are written in first person from the student's view: "I have submitted my work as a PDF."
- American spelling. "Georgia Tech" on first mention, "Tech" afterward is fine. "Team Leader" (capitalized) for the undergraduate assistant.
- Dates in prose and subtitles: full month, no year when obvious (`September 11`). Dates in tables and schedules: abbreviated (`Aug. 28`, `Sept. 4`, `Oct. 2`, `Nov. 6`, `Dec. 4`; note **Sept.**). Lecture front matter: `date: "September 18, 2026"`.
- Times: `11:59 PM ET`, ranges with `&ndash;`. Deadlines are 11:59 PM ET unless stated otherwise.
- Grades: `10% of course grade`, points as plain numbers. Percent weights and points in pages must match the syllabus.
- Submission filenames are given in code formatting: `` `Lastname-Firstname-Resume.pdf` ``, `` `Team-Name-Contract.pdf` ``. Work is submitted to Canvas as PDF.
- Unfinished content: `TBD` in rendered text plus an HTML comment `<!-- TODO: ... -->` in the source explaining what is missing.
- Keep facts consistent everywhere they appear. When a date moves, update the schedule in `index.qmd`, the assignment page (subtitle and body), the category/overview table, any lecture "Due dates" slide, and lecture speaker notes; then grep for the old date.

## Page structure (website pages)

- Front matter is `title` + `subtitle` only.
  - Course pages (index, syllabus, supplemental, lecture index): `subtitle: "<COURSE>: <Course Name>"`.
  - Assignment pages: `subtitle: "Due: <Month D> by 11:59 PM ET &middot; <N>% of course grade"`.
- Headings: `##` Title Case for page sections (numbered automatically by `number-sections: true`). Do not use `#` in the body.
- Assignment page section order: **Purpose**, then any assignment-specific sections, **What to Submit**, **Expectations**, **Submission Checklist**, **Helpful Resources** (the last two may be swapped, but keep them at the end).
- Point tables: `| Deliverable | Due | Points | |` with a `[Open assignment](...)` link column and a bold **Total** row.
- Callouts: `{.callout-note}` for info, `{.callout-tip}` for advice, `{.callout-important}` for rules and deadlines, `{.callout-warning}` sparingly. Two-column layouts use `:::: {.columns}` with `::: {.column width="50%"}`.
- Links between pages are relative paths to the `.qmd` source (`../supplemental/resume-cv.qmd`), never to `.html`.
- Citations use keys from `references.bib` (`[@key]`); the bibliography is project-wide.
- New pages must be added to the navbar in `_quarto.yml` (and lectures to `lectures/index.qmd`).

## Lecture slides (RevealJS)

- File name `lectures/lecture-NN.qmd` (two digits, numbered by lecture). Add a row to `lectures/index.qmd`: `| N | Mon. D | Topic | [Open slides](lecture-NN.qmd){target="_blank"} |`.
- Front matter (copy from the previous lecture and keep identical apart from title, subtitle number, and date):

  ```yaml
  title: "Topic Title"
  subtitle: "<COURSE> &middot; Lecture N"
  author: "Andrew J. Steinmetz"
  date: "Month D, YYYY"
  format:
    revealjs:
      theme: [default, gatech-revealjs.css]
      slide-number: c/t
      transition: none
      footer: "<see repo-specific footer below>"
      width: 1200
      height: 750
      auto-stretch: false
  ```

  Slide size stays 1200 x 750 (16:10).
- One slide per `##` heading, with `---` on its own line between slides.
- Slide titles are **sentence case** (unlike page headings): "Writing strong bullets", "Where do new physics PhDs work?". Capitalize the first word after a `Part N:` or `Aside:` label ("Part III: The graduate school path"); after any other colon, lowercase ("Study abroad: the deadlines are earlier than you think"). Proper nouns and official names keep their capitals: GT 1000, NSF GRFP, PhD, CV, Team Leader, Fall 2026 All Majors Career Fair, assignment names (Campus Scavenger Hunt), and the majors Physics, Astrophysics, and Applied Physics.
- Usual opening: a "Due dates"/"Upcoming" slide with a `| What | When | Points |` table. Usual close: a `## References` slide containing `::: {#refs}` (add `{.scrollable}` and `style="font-size: 0.7em;"` when long).
- Section dividers: `## Part II: Sentence-case title {.section-slide background-color="#003057"}`.
- Slide building blocks (styled in `lectures/gatech-revealjs.css`):
  - `::: {.highlight-box}` for the key takeaway (hyphen, not underscore).
  - `::: {.cite-note}` under a figure or claim for its source, e.g. `Source: [@key]`.
  - `::: {.nonincremental}` around lists.
  - `::: notes` for speaker notes: sourcing details, reminders, things to re-check before class.
- Figures live in `lectures/figs/` (decorative images in `lectures/figs/fluff/`), inserted as `![](figs/name.png){fig-align="center" width="80%"}` with `fig-alt` text for meaningful images.
- The cream outline on `.reveal .slides` marks the slide frame for spotting overflow; keep content inside it.

## Styling

- Site theme `gatech-theme.css` and slide theme `lectures/gatech-revealjs.css` are **identical in both repos**. Change them in both.
- Colors come from the CSS variables (Georgia Tech navy `#003057`, gold `#B3A369`, bright gold `#EAAA00`, cream `#f9f6e5`). Prefer an existing class over inline `style=`; keep inline styles to small font-size or alignment tweaks.

## Directory structure

```
index.qmd                 Welcome page; its Course Schedule is the live, authoritative schedule
_quarto.yml               Site config and navbar
gatech-theme.css          Site theme (shared across both repos)
references.bib            Project-wide bibliography
course-files/             Syllabus (.qmd) and LaTeX sources (*-latex/ folders: printable syllabus, worksheets)
assignments/              Assignment pages
supplemental/             Reference guides (resume-cv, technical-writing, peer-feedback)
lectures/                 index.qmd, lecture-NN.qmd, gatech-revealjs.css, figs/
_site/, _freeze/, .quarto/  Build output (not edited by hand)
```

LaTeX files in `course-files/*-latex/` are named `<course>-<topic>[-<term>].tex` (e.g. `gt-1000-syllabus-fall26.tex`).

## This repo: gt-phys-4604 (PHYS 4604, Professional Development)

- Course: PHYS 4604 Professional Development, Fall 2026, 1 credit. Audience: final-year Physics, Astrophysics, and Applied Physics majors preparing for graduate school or industry.
- Course-page subtitle: `"PHYS 4604: Professional Development"`. Lecture subtitle: `"PHYS 4604 &middot; Lecture N"`.
- Lecture footer: `"PHYS 4604 &middot; Fall 2026 &middot; Georgia Institute of Technology"`.
- Assignments are flat in `assignments/`, one page each, titled with their number: `title: "Assignment 3 &middot; Research Proposal"`.
- Several pages link to Canvas pages (course 559356), e.g. the AI Usage Statement; keep those links rather than duplicating Canvas content.
- `lectures/lab-report.qmd` is a guest deck for PHYS 4321/4322 (Advanced Lab): its own subtitle and footer (`"PHYS 4321/4322 &middot; Georgia Institute of Technology"`), no date, and `code-overflow: wrap`. It is not part of the numbered lecture sequence.
- Lectures without slides (guest speakers) still get a row in `lectures/index.qmd` with `--` in the Slides column.
- `_old/` holds the archived original HTML pages. Reference only; do not edit.
- `submissions/` (if present) holds student work. It is gitignored and must never be committed, published, or quoted outside this machine.
