# KNU Master's Thesis LaTeX Template

[한국어 안내](README.ko.md)

> **Notice:** This is an unofficial template. It is not officially distributed by Kyungpook National University or its School of Electronic and Electrical Engineering. Always follow the officially distributed thesis format and submission guidelines provided by the university and your school or department; those requirements take precedence over this template.

> **Paper size:** This template produces a PDF in **190 × 260 mm (4×6 baepan)** format, **not standard A4 (210 × 297 mm)**. The dimensions are specified in the `geometry` settings in `thesis.sty`. Confirm this size when printing or binding, and select **Actual size (100%)** to preserve the intended dimensions. Selecting “Fit to A4” may enlarge the document or change its placement.

A LaTeX template for a Master of Science thesis at Kyungpook National University (KNU), adapted from the [PhD Thesis Template - KNU on Overleaf](https://www.overleaf.com/latex/templates/phd-thesis-template-knu/wzwwnhnmbdjq) by **Gwenaelle Cunha Sergio** and **Dennis Singh Moirangthem**. It includes covers, a committee approval page, contents, lists of figures and tables, references, and English and Korean abstracts.

This version uses XeLaTeX, TeX Gyre Termes for the main Latin font, and font files in `fonts/` for Korean text and cover typography. Check the final layout against your department's submission requirements.

## Environment setup

### Local installation

Install a TeX distribution with **XeLaTeX**, **BibTeX**, **latexmk**, and **ko.TeX** (Korean typesetting). On Ubuntu/Debian, a practical starting point is:

```bash
sudo apt update
sudo apt install latexmk texlive-xetex texlive-lang-korean \
  texlive-latex-extra texlive-fonts-recommended texlive-publishers tex-gyre
```

On macOS, install [MacTeX](https://www.tug.org/mactex/). On Windows, install [TeX Live](https://www.tug.org/texlive/) or [MiKTeX](https://miktex.org/), with the equivalent packages. The bibliography uses `IEEEtran.bst`; use BibTeX, not Biber.

Open a terminal in the directory containing `thesis.tex` and check:

```bash
xelatex --version
bibtex --version
latexmk --version
kpsewhich kotex.sty
kpsewhich IEEEtran.bst
```

Keep the `fonts/` directory beside `thesis.tex`. The style loads these files directly, so system-wide font installation is unnecessary:

- `batang.ttc`
- `unbatang-IT.ttf`
- `malgungothic-R.ttf`, `malgungothic-BD.ttf`, `malgungothic-IT.ttf`

### VS Code (optional)

Open this directory as a folder and install the recommended **LaTeX Workshop** extension (`james-yu.latex-workshop`). The included `.vscode/settings.json` runs XeLaTeX on file changes. Use **LaTeX Workshop: Build LaTeX project** with `thesis.tex` active.

The supplied recipe performs only one XeLaTeX pass; it does not run BibTeX. For a complete bibliography and updated cross-references, use the terminal build below. If building a file in `tex/` separately selects the wrong root, open `thesis.tex` before building.

### Overleaf

Upload the source files together with `tex/`, `figures/`, and `fonts/` into an Overleaf project. Set the main document to `thesis.tex` and the compiler to **XeLaTeX**, then recompile. Generated local files such as `.aux`, `.bbl`, and `thesis.pdf` are not needed for the upload.

## Build

Run from the directory containing `thesis.tex`:

```bash
latexmk -xelatex -interaction=nonstopmode -file-line-error thesis.tex
```

The output is `thesis.pdf`. Alternatively, run the full sequence manually:

```bash
xelatex -interaction=nonstopmode -file-line-error thesis.tex
bibtex thesis
xelatex -interaction=nonstopmode -file-line-error thesis.tex
xelatex -interaction=nonstopmode -file-line-error thesis.tex
```

To remove intermediate build files while keeping the PDF:

```bash
latexmk -c thesis.tex
```

## Using the template

1. **Fill in thesis information** in `thesis.tex`: `\title`, `\author`, `\submitdate`, `\supervisor`, `\department`, and committee members `\profA`, `\profB`, `\profC`. Set `\titlekorean`, `\authorkorean`, `\supervisorkorean`, and `\departmentkorean` as well. Use `\\` for explicit line breaks where needed. The cover already adds “Supervised by Professor” before the supervisor field.
2. **Replace the example body** in `tex/introduction.tex`, `tex/sections.tex`, `tex/adding_equations.tex`, `tex/adding_refs.tex`, and `tex/conclusion.tex`. The template uses the `article` class: start main divisions with `\section`, not `\chapter`.
3. **Write both abstracts** in `tex/abstract_english.tex` and `tex/abstract_korean.tex`, replacing the filler text. The English abstract's school name is currently hard-coded in `\makeabstractheader` in `thesis.sty`; edit it there if needed.
4. **Add references** to `bibliography.bib` and cite their keys, for example `\cite{lin2004rouge}`. Run the complete build after changing citations.
5. **Add figures** under `figures/`, and use `\includegraphics`, `\caption`, and `\label`; see `tex/sections.tex` for examples.

To add a new section, create a file such as `tex/method.tex`:

```latex
\section{Method}\label{sec:method}
Describe your method here.
```

Then insert it in `thesis.tex` at the desired position, following the existing counter-reset convention:

```latex
\setcounter{figure}{0}
\setcounter{table}{0}
\input{tex/method} \pagebreak
```

| Path | Purpose |
| --- | --- |
| `thesis.tex` | Main document, metadata, and section order |
| `thesis.sty` | Page layout, cover macros, fonts, and headings |
| `tex/packages.tex` | Additional LaTeX packages |
| `tex/` | Body sections and abstracts |
| `bibliography.bib` | BibTeX entries |
| `figures/` | Figure assets |
| `fonts/` | Font files loaded by the style |
| `.vscode/` | Shared editor configuration |

If compilation reports `fontspec` errors, confirm that you selected XeLaTeX. For missing font files, check `fonts/` and run from the project directory. If references appear as `?`, run the full build and check that the cited keys exist in `bibliography.bib`.

## Copyright and license

Original template copyright © **Gwenaelle Cunha Sergio** and **Dennis Singh Moirangthem**. The [Overleaf source](https://www.overleaf.com/latex/templates/phd-thesis-template-knu/wzwwnhnmbdjq) identifies its license as **Creative Commons Attribution 4.0 International (CC BY 4.0)**.

This adaptation changes the degree wording to Master of Science, adjusts Korean fonts and layout, adds circled approval marks and editor configuration, and documents local usage. Original copyright notices remain in the source. See [LICENSE](LICENSE) for attribution, license links, and scope. Font files and other third-party assets retain their own applicable terms; the template license does not establish their redistribution rights.
