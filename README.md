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
