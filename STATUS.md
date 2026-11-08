# STATUS.md

## What was built

**nursing-care-plan-walkthrough-guide** — a beginner-friendly walkthrough that teaches nursing students how to build nursing care plans "like a friend would explain them": assessment cues, NANDA-style diagnosis language, SMART goals, interventions, and evaluation.

**What it is:** education only. **What it is not:** medical advice, a clinical decision tool, a charting/documentation template, or a place for real patient data. This is stated on the site landing page, in every chapter, in the worksheet, and in the README.

### Distinctness

Deliberately distinct from the sibling projects:
- *sbar-report-builder-webapp* builds shift-report/communication artifacts; this project teaches a different skill (whole care-plan thinking: diagnose → goal → intervene → evaluate) and is a guide + worksheet, not a report generator.
- *nclex-style-quiz-trainer* drills exam questions; this project has no quizzes — it is a linear walkthrough with a worked example and a blank practice worksheet.

### Files

```
README.md                          Landing doc, chapter map, disclaimer, credit
LICENSE                            MIT — Copyright (c) 2026 Asdale Dynamics, LLC
STATUS.md                          This file
docs/00-read-me-first.md           Ground rules, how the guide fits together
docs/01-assessment-cues.md         Cues: subjective/objective, strong vs. weak, clustering
docs/02-nanda-style-language.md    PES pattern, common mistakes, 3 diagnosis types
docs/03-smart-goals.md             SMART structure, scoring test, fix-the-weak-goal drills
docs/04-interventions.md           Independent vs. collaborative, worst/better/best, alignment
docs/05-evaluation.md              Met/partially met/unmet, the revise loop
docs/06-worked-example.md          One complete fictional plan, all five steps
docs/07-glossary-cheatsheet.md     Glossary, blueprint diagram, pre-submission checklist
site/index.html                    Static landing page (chapter map + links + disclaimer)
site/worksheet.html                Blank care-plan worksheet (fillable + print-friendly)
```

## How to run it

- **No build step, no dependencies, no network.** Everything is plain Markdown + hand-written HTML/CSS.
- Read the guide: open `README.md` (or the `docs/` chapters in order).
- Use the site: open `site/index.html` in any browser (double-click it or `open site/index.html` / `xdg-open site/index.html`).
- Worksheet: from the landing page click "Open the blank worksheet," or open `site/worksheet.html` directly. It is fillable on screen, has a print button (CSS `@media print` disables chrome and keeps the form), and a "Clear everything" button. Nothing is saved, transmitted, or stored — by design, so no patient data can linger. Print output is paper-only.
- Optional local preview of the markdown: any markdown reader, e.g. `python3 -m http.server` in the repo root won't render .md, but the site links to the raw `docs/*.md` files which display fine in modern browsers, or use any preferred md viewer.

## Verification results

Ran on the copy in this folder:

1. **All files present and non-empty** — `find` + `wc -l` checks pass for 8 docs, 2 HTML pages, README, LICENSE, STATUS.md.
2. **Copyright line exact** — `grep "Copyright (c) 2026 Asdale Dynamics, LLC" LICENSE` matches exactly once, as required. README and site footer credit Asdale Dynamics, LLC.
3. **HTML sanity** — both pages checked with a tag-balance script (every opening tag has a matching closing tag, no unclosed `<div>`/`<section>`/`<table>`/`<textarea>`). Both balanced. Scripts on the worksheet verified working in-browser (clear function + onclick handlers, no console errors).
4. **No secrets / no personal data** — targeted regex scans for credential patterns (`api_key=`, `password:`, `token:`, PEM key blocks) return no credentials; the only regex matches were ordinary English words ("secretions", "the two-column secret"). All examples are fictional placeholders (`[date]`, `[time]`, invented case-study scenarios).
5. **Dead-link check (internal)** — all relative hrefs from `site/index.html` (`docs/*.md`, `worksheet.html`) and from `docs/` cross-references resolve to real files on disk.
6. **Git** — initialized, all files committed with the existing local identity, plain commit message, no Co-authored-by trailers, no remote configured, never pushed.

## Known gaps

- **Linking from HTML pages to markdown chapters:** browsers download or display `docs/*.md` as plain text; if you want prettier chapter pages, they'd need .html copies — kept raw on purpose (local-first, zero build).
- NANDA-I exact wording changes by edition; the guide teaches the PES *pattern* and repeatedly points to the student's program-approved reference rather than endorsing specific labels covering every case.
- The worked example covers one diagnosis (impaired walking). Only one full worked example so far — more for other diagnosis flavors (risk, health-promotion) would strengthen it.
- No PDF export of the worksheet beyond the browser's native print-to-PDF.
- Accessibility: forms are labeled and semantic, but a screen-reader pass and WCAG audit have not been done.

## Compliance notes

- Education-only disclaimers on the site, in every doc, in the README, and in the worksheet.
- No patient data fields that persist anything; worksheet is cleared on tab close and offers explicit Clear.
- No secrets, API keys, or personal data anywhere in the repo.
- MIT LICENSE with the exact required copyright line; README credits Asdale Dynamics, LLC.
