# Academic CV — Design Spec

Date: 2026-09-21

## Goal

Adapt Geoff Boeing's LaTeX academic CV template (this fork) into Ben Drusinsky's
academic CV. It is for PhD/academic applications (PK NRW 2026 first) and lives
alongside Ben's separate practice-oriented CV. Style follows Boeing's as closely
as possible: no role descriptions, terse one-line entries, Education first.

## Files

| Action | File |
|---|---|
| Rename + rewrite | `cv-gboeing.tex` → `cv-drusinsky.tex` |
| Edit | `.github/workflows/build_publish.yml` — build + upload PDF as workflow artifact; remove S3/AWS steps |
| Edit | `README.md` — describe this CV; keep credit/link to Boeing's original |
| Edit | `LICENSE.txt` — add Ben's copyright line above Boeing's (MIT requires keeping his) |
| Keep | `.gitignore`, `.pre-commit-config.yaml` unchanged |

## Preamble changes only

Keep the preamble verbatim except:

- `\myname` → `Ben Drusinsky`
- `pdfkeywords` → `computational design, media archaeology, critical making,
  human-computer interaction, permacomputing, architecture`
- Header comment block (name/email/web/repo)

## Header block

Name (`\namefont`), then two minipages:

- Left: `Köln International School of Design \\ TH Köln \\ Köln, Germany`
- Right: `ben.drusinsky@th-koeln.de \\ +31 648432257 \\ bendrusinsky.com`
  (email and site as `\href`)

No tagline, no home city.

## Sections, in order

All entries use `tablist` (`\item[YEAR] \tab{}…`) unless noted as `itemize`.
Titles in `\enquote{}`; DOIs as `\href`; year ranges with `--`; ongoing as `2025--`.

### Education

```
PhD    Design, Köln International School of Design (TH Köln) and Winchester
       School of Art (University of Southampton), in progress (2025--)
MDes   Industrial Design, Design and Technology, Bezalel Academy of Arts and
       Design, and DLX Lab, University of Tokyo, 2022
BArch  (MArch equivalent), Bezalel Academy of Arts and Design, 2018
```

### Appointments (institution line, then roles on continuation lines)

```
2025--    TH Köln
          Adjunct Lecturer, Code and Context BSc, Faculty of Computer Science
          Adjunct Lecturer, Köln International School of Design (Integrated Design BA/MA)
2021--23  Technion -- Israel Institute of Technology
          Associate Researcher, Horizon Europe SONATA project
2020--23  Bezalel Academy of Arts and Design
          Adjunct Lecturer and Academic Coordinator, School of Architecture
```

### Research Areas (`itemize`, verbatim)

- Media archeology and critical making
- Human-computer interaction, permacomputing and computation within limits
- Architecture history and theory

### Publications › Conference Proceedings

```
2026  B. Drusinsky. "When Beds Stopped Working." Proceedings of the 14th Conference
      on Computation, Communication, Aesthetics & X. Turin, Italy. In press.
2025  B. Drusinsky, L. Scherffig, T. Dillon, and C. Höfer. "In Every Dream Home an
      Internet." Mensch und Computer 2025 Workshops. doi:10.18420/muc2025-mci-ws14-175
2024  B. Drusinsky, S. Grodsky, E. Haiman, and D. Schaumann. "A Simulation Framework
      for Space-Use Alignment in Adaptive Environments." Proceedings of eCAADe 2024.
      doi:10.52842/conf.ecaade.2024.1.653
2023  D. Schaumann, N. Duvdevani, A. Elya, I. Levin, T. Sofer, B. Drusinsky, et al.
      "Coupling Co-presence in Physical and Virtual Environments Toward Hybrid Places."
      CAAD Futures 2023. doi:10.1007/978-3-031-37189-9_35
```

("et al." stays until Ben supplies the full author list.)

### Invited Talks (flat list, no subsections)

```
2026  "Computer Room and Other Stories: Breaking LLMs as a Design Practice."
      Learning to Teach: (Re)designing Creative Tech Pedagogy symposium,
      NYU Tandon Integrated Design & Media. New York (virtual). Jan.
2025  "In Every Dream Home an Internet." Update: Blue Shift Symposium,
      Riga Technical University. Liepāja, Latvia. Oct.
2025  "NolliGAN: Generative Mapping as Spatial Exploration." Transform 2025:
      Conference on AI, Art and Society, Hochschule Trier. Trier, Germany. Sept.
2025  "Computational Design for Mapping Sentiment Analysis." CDFAM Computational
      Design Symposium. Amsterdam, Netherlands. Jul.
2025  "In Every Dream Home an Internet." design:promoviert, DGTF Doctoral Research
      Colloquium, HTW Dresden. Dresden, Germany. Jun.
2025  "NolliGAN: Generative Mapping as Spatial Exploration." Livingmaps Network
      Conference: More-than-Human Mapping, University of London. London, England. Apr.
```

### Conference Activity › Workshops Organized

```
2026  "Local LLMs for Design Research: Considerations for Ethical and Environmental
      Use of AI." By Design and By Disaster, Free University of Bozen-Bolzano.
      Bolzano, Italy. May.
2025  "Build Your Own AI Companion: Hacking AI with Low-Tech Computing."
      Update: Blue Shift Symposium, Riga Technical University. Liepāja, Latvia. Oct.
2025  "Local LLMs for Design Research: Considerations for Ethical and Environmental
      Use of AI." design:promoviert, DGTF Doctoral Research Colloquium, HTW Dresden.
      Dresden, Germany. Jun.
```

### Conference Activity › Conference Papers Presented

```
2026  B. Drusinsky. "When Beds Stopped Working." 14th Conference on Computation,
      Communication, Aesthetics & X. Turin, Italy. Jul.
2025  B. Drusinsky, L. Scherffig, T. Dillon, and C. Höfer. "In Every Dream Home an
      Internet." Mensch und Computer 2025. Chemnitz, Germany. Sept.
2024  B. Drusinsky, S. Grodsky, E. Haiman, and D. Schaumann. "A Simulation Framework
      for Space-Use Alignment in Adaptive Environments." eCAADe 2024. Nicosia, Cyprus. Sept.
```

### Exhibitions and Residencies › Residencies and Hackathons

```
2026     TeleAgriCulture hackathon. DFKI, Berlin, Germany. Jun.
2026     TeleAgriCulture hackathon. V2_ Lab for the Unstable Media, Rotterdam, Netherlands. Apr.
2025--26 Microdosing AI, artist residency. V2_ Lab for the Unstable Media,
         Rotterdam, Netherlands. Dec--Mar.
2025     Mirage, algorithmic performance residency. V2_ Lab for the Unstable Media,
         Rotterdam, Netherlands. Oct--Nov.
```

### Exhibitions and Residencies › Exhibitions and Performances

```
2026  Rotterdam Art Week, live performance commission. De Achtertuin,
      Rotterdam, Netherlands. Mar.
2025  TurgotGAN. BYOD², Shibuya, Tokyo, Japan. Feb.
2023  BillYourSelf. Jerusalem Design Week. Jerusalem, Israel. Jul.
2021  NolliGAN. The WRONG Biennale. Barcelona, Spain / online. Aug.
```

### Courses Taught (`itemize` per institution; names only, no years)

TH Köln
- Introduction to Physical Computing (Code and Context BSc)
- Computer Room (Köln International School of Design)

Bezalel Academy of Arts and Design
- The Productive Superblock, with Dr. Aiman Tabony
- The Dictionary of Political Ideas, with Dr. Erez Golany Solomon
- Building Systems as Technology (teaching assistant)

### Languages (`itemize`)

- English (native), Hebrew (native)

### Professional Employment

```
2026--    Senior Computational Designer and AI Integration Lead, HQA, Tel Aviv, Israel (remote)
2024--    Co-founder, Urban Futures Lab, The Hague, Netherlands
2022--25  Senior Computational Designer and Architect, YGAA, Tel Aviv, Israel (remote)
2018--21  Senior Architectural Designer, DY-CommonPlanning, Jerusalem, Israel
```

### Footer

`Updated \monthyeardate\today` — unchanged from template.

## Sections from the template deliberately omitted

Book Chapters, Journal Articles, Edited Articles, Reports, Patents, Keynotes,
Sessions Organized, Session Chair, Invited Panelist, Grants and Awards, Service,
Peer Review, Memberships, Credentials, Consulting. Re-add later by copying the
template's block for that section.

## Build pipeline

- **CI**: on push to `main` (and manual dispatch), `xu-cheng/latex-action@v4`
  compiles `cv-drusinsky.tex`; `pdfsizeopt` compresses; `actions/upload-artifact`
  stores `cv-drusinsky.pdf`. No AWS steps, no `id-token` permission.
- **Local**: install BasicTeX via Homebrew plus the packages the preamble needs
  (`ebgaramond`, `tgheros`, `csquotes`, `microtype`, `datetime`, `enumitem`,
  `tabto`, `titlesec`, `nag`, `fmtcount`). Build with `pdflatex cv-drusinsky.tex`
  (run twice). PDF is gitignored.

## Verification

1. `pdflatex` completes with no errors; warnings reviewed.
2. Every entry from the spec appears in the PDF text (`pdftotext` diff against a
   checklist).
3. Layout visually matches Boeing's: same fonts, heading style, tab alignment.
4. Push to a branch; confirm the GitHub Action produces the artifact.

## Open items (build proceeds with defaults)

| Item | Default used |
|---|---|
| PhD faculty/field wording | "Design, KISD (TH Köln) and WSA (Southampton)" |
| 2023 paper full author list | keep "et al." |
| German language level | omitted |
| Awards / peer review / memberships / license | none |
| Upcoming talks | added when Ben supplies them |
