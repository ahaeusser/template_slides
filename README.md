# LaTeX Beamer slide template

A reusable 16:9 template based on the original slide deck. The Boadilla
theme, Latin Modern fonts, square bullets, frame-number footer, caption
styling, and automatic section outlines are retained. The title page is
left-aligned, and the primary color is SteelBlue (`#4682B4`).

## Files

```text
template_slides.tex       Main document and slide order
config/
  metadata.tex           Title, subtitle, author, affiliation, contact, date
  preamble.tex           Packages, existing design, reusable helpers
slides/
  01_basics.tex          Single-column bullets and numbered list
  02_columns.tex         Nine examples with two through five columns
  03_elements.tex        Figure, table, equation, and citation examples
  blocks.tex             Standard, example, and alert block examples
  04_closing.tex         Summary, questions, and references
  05_appendix.tex        Additional material
references.bib           Fictional bibliography placeholders
figures/                 Location for your own image files
```

## Start a new presentation

1. Edit `config/metadata.tex`.
2. Copy the frames you need from `slides/` and replace the dummy content.
3. Rename the sections, remove unused examples, and update the inputs in
   `template_slides.tex` if you add or rename slide files.
4. Replace figure placeholders and fictional bibliography entries.
5. Compile `template_slides.tex` from the project root.

All main example content is generic. The old research figures are retained
in `figures/` for safekeeping but are not used by the template. They may be
removed when you no longer need them.

## Column examples

| Columns | Examples | Width of each column |
| --- | --- | --- |
| 2 | Equal text columns | 0.48 / 0.48 |
| 2 | Narrow text and wide figure | 0.28 / 0.68 |
| 2 | Wide table and narrow text | 0.62 / 0.34 |
| 3 | Text; figures above text | 0.31 each |
| 4 | Text; figures with short labels | 0.23 each |
| 5 | Short bullets; figures with short labels | 0.18 each |

Widths are fractions of `\textwidth`. Each layout reserves space for gaps.
`columns[T,onlytextwidth]` keeps content top-aligned within the existing
slide margins. Use `\linewidth` when sizing an image inside a column.
Keep text short in four- and five-column examples to retain the original
body font size.

## Figures

The template builds without any external figures. Replace a command such as

```latex
\figureplaceholder[4cm]{Figure placeholder}
```

with your own image:

```latex
\includegraphics[width=\linewidth,height=4cm,keepaspectratio]
    {figures/your-figure.pdf}
```

The optional argument of `\figureplaceholder` controls its height.

## Build

Use pdfLaTeX and BibTeX, matching the original setup. With a TeX distribution
and latexmk installed, run from this folder:

```text
latexmk -pdf -interaction=nonstopmode -halt-on-error template_slides.tex
```

Alternatively, run:

```text
pdflatex template_slides.tex
bibtex template_slides
pdflatex template_slides.tex
pdflatex template_slides.tex
```

The result is `template_slides.pdf`. Compile the main file, rather than an
individual file in `slides/`. Repeat the complete build when changing the
bibliography or sections so citations, outlines, and total frame counts
update correctly.

## Design settings

Design settings are grouped in `config/preamble.tex`. Change the
`steelblue` color definition there to update the primary color. Standard
blocks use a steel-blue header with a light body. Example and alert blocks
keep the theme's green and red accents. The title-page template aligns the
title, subtitle, author, affiliation, and date to the left.

Each slide heading shows the current section in a smaller line above the
bold frame title. For example, a slide in `\section{Basic slides}` with
`\begin{frame}{Single-column layout}` automatically shows "Basic slides"
above "Single-column layout". Outline slides show only the bold title
"Outline", without a section label. Use `\outlineframe` for a full agenda
and `\outlineframe[currentsection]` for a section agenda. The presentation
title page keeps its separate layout. An optional `\framesubtitle{Custom label}` overrides the automatic
section label for an individual frame.

Content and metadata can be edited independently of those settings. Section outline
slides still appear automatically, and appendix slides retain frame numbers.
