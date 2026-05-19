# gt-phys-4604

PHYS 4604 — Professional Development

This repository contains course materials for PHYS 4604 (Professional Development), a 1-credit, in-person course offered at the School of Physics, Georgia Institute of Technology. Materials include the syllabus, welcome page, assignment pages, supplemental guides, and lecture files intended for students and instructors.

The site is built with [Quarto](https://quarto.org/). Project configuration is in `_quarto.yml`; visual styling is in `gatech-theme.css`. The live course site is hosted at **[ajsteinmetz.github.io/GT-PHYS-4604](https://ajsteinmetz.github.io/GT-PHYS-4604/)** via GitHub Pages.

## Contents

- `course-files/` — core course pages:
  - `syllabus.qmd` — full syllabus and course policies
  - `ai-usage-statement.qmd` — AI usage statement guidelines
  - `syllabus-latex/` — LaTeX source for the printable syllabus PDF
- `assignments/` — Quarto source for individual assignment pages:
  - `resume.qmd` — Résumé Assignment (10%)
  - `online-profile.qmd` — Online Profile Assignment (4%)
  - `research-proposal.qmd` — Research Proposal, GRFP Style (15%)
  - `personal-statement.qmd` — Personal Statement or Cover Letter (15%)
  - `external-participation.qmd` — External Participation Assignment (4%)
- `supplemental/` — additional reference guides:
  - `resume-cv.qmd` — Résumé vs. Academic CV
  - `technical-writing.qmd` — Technical and Professional Writing
- `lectures/` — lecture slides (Quarto RevealJS) and lecture index
- `_old/` — archived original HTML files

## Prerequisites

- [Quarto](https://quarto.org/docs/get-started/) 1.4 or later

No R or Python installation is required. All course materials are plain Markdown with no executable code blocks.

## Local Development

To render the full site locally:

```bash
quarto render
```

Rendered output is written to `_site/`. To preview the site in a browser with live reload:

```bash
quarto preview
```

To render a single file:

```bash
quarto render assignments/resume.qmd
```

Quarto uses `freeze: auto` (configured in `_quarto.yml`), so unchanged files are not re-rendered on subsequent runs. To force a full re-render, delete the `_freeze/` directory before running `quarto render`.

## Publishing

The site is deployed to GitHub Pages from the `gh-pages` branch. To publish:

```bash
quarto publish gh-pages
```

Quarto will render the project, update the `gh-pages` branch, and push to the remote. GitHub Pages then serves the updated site at [ajsteinmetz.github.io/GT-PHYS-4604](https://ajsteinmetz.github.io/GT-PHYS-4604/) within a few minutes.

The `gh-pages` branch contains only rendered output and should not be edited directly.

## Semester Rollover

At the end of each semester, tag the repository to preserve a snapshot before updating for the next term:

```bash
git tag fall-2026
git push origin fall-2026
```

Then update the semester, CRN, and schedule dates in `index.qmd` and `course-files/syllabus.qmd`, add any new lectures to `lectures/index.qmd`, and republish.
