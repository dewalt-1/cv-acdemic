# Academic CV Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Turn the forked Boeing CV template into `cv-drusinsky.tex`, compiled locally and by GitHub Actions to a workflow artifact.

**Architecture:** Single LaTeX file; preamble kept verbatim from the template, body rewritten from the spec. CI workflow trimmed to build + artifact upload. README/LICENSE updated for the new owner.

**Tech Stack:** pdflatex (BasicTeX via Homebrew), `xu-cheng/latex-action@v4`, `actions/upload-artifact@v4`.

## Global Constraints

- Spec: `docs/superpowers/specs/2026-09-21-academic-cv-design.md` — content of every section is defined there and must be reproduced exactly.
- Work on branch `drusinsky-cv`; never commit to `main`.
- `*.pdf` stays gitignored.
- Keep Boeing's MIT copyright line in `LICENSE.txt`.

---

### Task 1: Local TeX toolchain, verify template builds

**Files:** none changed.

- [ ] **Step 1: Install BasicTeX and required packages**

```bash
brew install --cask basictex
eval "$(/usr/libexec/path_helper)"
sudo tlmgr update --self
sudo tlmgr install ebgaramond tex-gyre csquotes microtype datetime fmtcount enumitem tabto-ltx titlesec nag setspace geometry hyperref babel-english
```

- [ ] **Step 2: Build the untouched template as a baseline**

Run: `cd /Users/bendrusinsky/Documents/Projects/CV && pdflatex -interaction=nonstopmode cv-gboeing.tex && pdflatex -interaction=nonstopmode cv-gboeing.tex`
Expected: exits 0, `cv-gboeing.pdf` produced. If a package is missing, the log names it (`! LaTeX Error: File 'X.sty' not found`) → `sudo tlmgr install <pkg>` and retry.

### Task 2: Write `cv-drusinsky.tex`

**Files:**
- Rename: `cv-gboeing.tex` → `cv-drusinsky.tex` (via `git mv`)
- Modify: the whole body of `cv-drusinsky.tex`; the header comment; `\myname`; `pdfkeywords`.

- [ ] **Step 1: `git mv cv-gboeing.tex cv-drusinsky.tex`**

- [ ] **Step 2: Replace lines 1–4 (header comment), line 32 (`\myname`), and line 95 (`pdfkeywords`)**

```latex
% Ben Drusinsky's Curriculum Vitae
% Email: ben.drusinsky@th-koeln.de
% Web: https://bendrusinsky.com/
% Repo: https://github.com/dewalt-1/cv-acdemic
% Template: https://github.com/gboeing/cv (MIT)
```
```latex
\newcommand{\myname}{Ben Drusinsky}
```
```latex
  pdfkeywords = {computational design, media archaeology, critical making, human-computer interaction, permacomputing, architecture},
```

- [ ] **Step 3: Replace everything from `\begin{document}` to `\end{document}` with the body**

Body content = spec sections in order, using these idioms exactly as the template does:
- `\section*{…}` / `\subsection*{…}`
- `\begin{tablist} … \item[YEAR] \tab{}… \end{tablist}` for dated lists
- `\begin{itemize} … \item … \end{itemize}` for flat lists
- `\enquote{Title.}` for titles, `\textit{}` for venue/proceedings names, `\href{https://doi.org/X}{doi:X}` for DOIs
- Multi-line appointments: institution on the `\item` line, roles on continuation lines ending in `\\`
- Footer block (`Updated \monthyeardate\today`) kept verbatim.

Full body is written in this task (see the committed file); it is the spec rendered into LaTeX, nothing more.

- [ ] **Step 4: Build**

Run: `pdflatex -interaction=nonstopmode cv-drusinsky.tex && pdflatex -interaction=nonstopmode cv-drusinsky.tex`
Expected: exits 0, no `!` errors in `cv-drusinsky.log`. Check overfull hbox warnings with `grep -c Overfull cv-drusinsky.log` — a couple are tolerable; fix any that push text into the margin.

- [ ] **Step 5: Verify content against spec**

Run: `pdftotext -layout cv-drusinsky.pdf - | less` and check every spec entry is present. Specifically confirm the 6 invited talks, 3 workshops, 3 papers presented, 4 proceedings, 4 residencies/hackathons, 4 exhibitions, 5 courses, 4 employment lines.

- [ ] **Step 6: Visual check**

Open the PDF (or render page 1 to PNG with `pdftoppm -png -r 80 -f 1 -l 1 cv-drusinsky.pdf page`) and compare against the Boeing PDF for fonts, heading style, tab alignment.

- [ ] **Step 7: Commit**

```bash
git add cv-drusinsky.tex
git commit -m "Rewrite CV content for Ben Drusinsky"
```

### Task 3: CI workflow → artifact upload

**Files:**
- Modify: `.github/workflows/build_publish.yml`

- [ ] **Step 1: Replace the file**

```yaml
---
name: Build PDF

on:  # yamllint disable-line rule:truthy
  push:
    branches: [main]
  pull_request:
  workflow_dispatch:

jobs:
  build_latex:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout repo
        uses: actions/checkout@v7

      - name: Build PDF
        uses: xu-cheng/latex-action@v4
        with:
          root_file: cv-drusinsky.tex

      - name: Compress PDF
        run: >
          docker run --rm -v "$PWD:/workdir" ptspts/pdfsizeopt
          pdfsizeopt cv-drusinsky.pdf cv-drusinsky.pdf

      - name: Upload PDF artifact
        uses: actions/upload-artifact@v4
        with:
          name: cv-drusinsky
          path: cv-drusinsky.pdf
```

(`pull_request` trigger added so the PR itself proves the build works.)

- [ ] **Step 2: Commit**

```bash
git add .github/workflows/build_publish.yml
git commit -m "Build PDF as workflow artifact instead of publishing to S3"
```

### Task 4: README and LICENSE

**Files:**
- Modify: `README.md`, `LICENSE.txt`

- [ ] **Step 1: Rewrite `README.md`**

```markdown
# Academic CV

Ben Drusinsky's LaTeX academic CV.

The TeX file is compiled to PDF by a [GitHub Actions workflow](.github/workflows/build_publish.yml) on every push to `main` and on pull requests; the PDF is attached to the workflow run as an artifact (`cv-drusinsky`). The PDF itself is not committed.

## Building locally

```bash
pdflatex cv-drusinsky.tex && pdflatex cv-drusinsky.tex
```

Requires a TeX distribution with `ebgaramond`, `tex-gyre`, `csquotes`, `microtype`, `datetime`, `enumitem`, `tabto`, and `titlesec`.

## Credit

Forked from [Geoff Boeing's academic CV](https://github.com/gboeing/cv), used under the MIT license. The formatting and LaTeX structure are his; the content is mine.
```

- [ ] **Step 2: Add a copyright line to `LICENSE.txt`** — insert `Copyright (c) 2026 Ben Drusinsky` directly above the existing `Copyright (c) 2017-2025 Geoff Boeing`.

- [ ] **Step 3: Commit and push**

```bash
git add README.md LICENSE.txt
git commit -m "Update README and license for fork"
git push -u origin drusinsky-cv
```

Then check the Actions tab: the push triggers nothing (branch isn't `main`), but opening the PR will. Open the PR only when Ben approves.
