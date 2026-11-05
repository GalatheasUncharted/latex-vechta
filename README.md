A LaTeX template for academic papers at the University of Vechta.

This repository provides a ready-to-use template for writing term papers, seminar papers and theses at the University of Vechta with LaTeX. It contains the complete page layout, starting with the cover page, as well as citation styles that are adapted to the requirements of the individual departments (for example History or English Studies).

> **Notice, declaration of independent work:** the declaration and the documentation of the AI applications you used are filled in digitally, directly in LaTeX. You do not have to print, fill in by hand, sign and scan anything. Open `chapters/00_examples/doiw.tex`, scroll to the bottom and follow the instructions in [Filling in the declaration digitally](#filling-in-the-declaration-digitally). Whether your examiner accepts a digitally completed declaration has to be clarified with them and the examination office beforehand.

> **Status:** work in progress. The structure described below is the target layout; not all parts are available yet.

## Features

- Modular setup: `main.tex` only loads packages and global settings and then imports every part of the paper (cover page, chapters, declaration of independent work).
- Separate cover page (`cover/cover.tex`) that can be edited without touching the rest of the document.
- Department-specific citation styles for `biblatex`, selectable with a single line in `main.tex`.
- Example chapter and example declaration of independent work as a starting point.
- Declaration of independent work (official form of the University of Vechta) that is filled in digitally, including checkboxes, free text and an image of your signature.
- Bibliography management with Zotero (see below), so that no references have to be typed by hand.

## Repository structure

```
latex-vechta/
├── main.tex                  Packages, settings, imports of all parts
├── sources/
│   └── lib.bib               Bibliography (biblatex), exported from Zotero
├── cover/
│   └── cover.tex             Cover page
├── chapters/
│   ├── 00_examples/          Example chapter and declaration of independent work
│   │   ├── example_chapter.tex
│   │   ├── doiw.tex          Declaration of independent work
│   │   └── doiw_preamble.tex Packages and settings for doiw.tex
│   ├── 01_Introduction/      Example: your first chapter
│   │   ├── index.tex         Only imports the subsections below
│   │   ├── preface.tex
│   │   ├── outline.tex
│   │   ├── methodology.tex
│   │   └── research_question.tex
│   ├── 02_Main_Part/         Example: your next chapter, same pattern
│   │   ├── index.tex
│   │   └── ...
│   └── 03_Conclusion/
│       ├── index.tex
│       └── ...
├── images/
│   ├── logos/
│   │   └── vechta/           University logos (logo_uni.pdf, logo_audit.pdf)
│   └── sign/                 Your signature (your_sign.png), dummy: example_sign.png
└── styles/
    ├── history/              Citation style for History Studies
    │   ├── history_vechta.bbx
    │   └── history_vechta.cbx
    └── english/              Citation style for English Studies
```

## Requirements

- A current TeX distribution (TeX Live or MiKTeX; the more recent, the better, because `biblatex` and Biber must match each other).
- A LaTeX editor, for example [TeXstudio](https://www.texstudio.org/).
- [Biber](https://github.com/plk/biber) as bibliography backend (included in TeX Live and MiKTeX). In TeXstudio, set the default bibliography tool to **Biber** under *Options, Configure TeXstudio, Build*.
- [Zotero](https://www.zotero.org/download/) with the plugin Better BibTeX (see below).

## Getting started

1. Clone this repository or download it as a ZIP file:
   ```
   git clone https://github.com/GalatheasUncharted/latex-vechta.git
   ```
2. Open `main.tex` in your editor and select the citation style for your department.
3. Put your personal data (title, name, student ID, module, lecturer) into `cover/cover.tex`.
4. Write your chapters in the `chapters/` folder and import them in `main.tex` (see [Structuring your chapters](#structuring-your-chapters)).
5. Compile in this order: LaTeX, Biber, LaTeX, LaTeX (TeXstudio does this automatically with the "Build & View" command when Biber is configured).

## Filling in the declaration digitally

The declaration of independent work (`chapters/00_examples/doiw.tex`) follows the official form of the University of Vechta (version 25-02-26) and is imported at the end of `main.tex`. Its packages and settings are loaded from `chapters/00_examples/doiw_preamble.tex`. Page 1 is the declaration itself, page 2 is the documentation of the AI applications you used ("Anhang: Dokumentation der verwendeten KI-Anwendungen").

### 1. Signature

Put an image of your signature (PNG, JPG or PDF) into `images/sign/` and name it `your_sign.png`. It is placed above the signature line on page 1 (height 30 pt). The file is ignored by Git, so your signature is not committed by accident.

The template ships with a dummy signature, `images/sign/example_sign.png`. It is used only as long as `your_sign.png` does not exist. **Before you hand in your work, make sure that your own signature is used** (or that you sign by hand), because otherwise the dummy signature "Student" appears in the PDF. If neither file exists, the space above the line stays empty.

### 2. Documenting AI applications

Open `chapters/00_examples/doiw.tex` and scroll to the bottom. There are two blocks, one for each application you used (as in the official form):

```latex
\ekKIBlock{Name and version of the application}{keys for the kind of use}
```

The first argument is the name and version of the model or application as free text, the second argument is a comma-separated list of keys. Both arguments may be empty.

Example:

```latex
\ekKIBlock{ChatGPT 5.2 (OpenAI)}{redaktion, recherche-literatur}
\ekKIBlock{Claude Sonnet 5.5 (Anthropic)}{struktur, sonstiges={Proofreading}}
```

Available keys for the kind of use (each key ticks the matching checkbox of the form):

| Key | Checkbox in the form (wording of the form in parentheses) |
| --- | --- |
| `struktur` | Structural: ideas and outline of the paper (*Strukturell (Ideen/Aufbau der Arbeit)*) |
| `redaktion` | Editorial revision (*Redaktionelle Überarbeitung*) |
| `recherche-literatur` | Research: literature (*Recherche (Literatur)*) |
| `recherche-inhalte` | Research: content (*Recherche (Inhalte)*) |
| `visualisierung` | Visualisation (*Visualisierung*) |
| `uebersetzung` | Translation (*Übersetzung*) |
| `sonstiges={text}` | Other, namely: *text* (*Sonstiges und zwar*; ticks the box and writes your text on the line) |

Rules:

- Use the key names exactly as written above (lowercase, `ue` instead of `ü`).
- Combine as many keys as you need, separated by commas.
- For `sonstiges`, put the text in curly braces, so that it may contain commas: `sonstiges={Proofreading, spell checking}`.
- Leave a block empty with `\ekKIBlock{}{}` if you want to fill it in by hand. The template ships with two empty blocks.
- If you did not use any AI application, leave both blocks empty.
- A long application name makes the line longer automatically.

### 3. Date and place

Date and place are set at the top of `chapters/00_examples/doiw.tex` with one command:

```latex
\ekDatumOrt{Vechta, 05.11.2026}
```

Remove the `%` in front of the prepared example line and adapt it. Use `\ekDatumOrt{Vechta, \today}` if the date of compilation should be inserted automatically. The text is printed on a line to the left of the signature; the label below the line reads "Datum, Ort und Unterschrift" (date, place and signature; the wording of the official form is kept in German). Without this command the place stays empty and the layout is identical to the official form, so that you can write date and place by hand.

### Summary: what you can fill in

| What | Where | How |
| --- | --- | --- |
| Signature | `images/sign/` | Save the image as `your_sign.png` |
| Date and place | top of `doiw.tex` | `\ekDatumOrt{Vechta, 05.11.2026}` |
| AI application 1 and 2 | bottom of `doiw.tex` | `\ekKIBlock{Name and version}{keys}` |

## Structuring your chapters

We recommend to separate your chapters strictly, both by number and by name. Every chapter gets its own folder (`<number>_<Name>`), and every folder contains an `index.tex` that does nothing but import the subsections of that chapter. `main.tex` then only imports the `index.tex` of each chapter.

In `main.tex`:

```latex
\input{chapters/01_Introduction/index}
\input{chapters/02_Main_Part/index}
\input{chapters/03_Conclusion/index}
```

In `chapters/01_Introduction/index.tex` (example):

```latex
\input{chapters/01_Introduction/preface}
\input{chapters/01_Introduction/outline}
\input{chapters/01_Introduction/methodology}
\input{chapters/01_Introduction/research_question}
```

Each subsection file (for example `preface.tex`) contains only its own text, starting with a `\section{...}` or `\subsection{...}` command, and no preamble.

Recommendations:

- Use a two-digit number as prefix, so that the folders are sorted in the order of your paper.
- Use only letters, digits, underscores and hyphens in file and folder names. Avoid spaces and umlauts, they cause problems on some systems.
- Always write paths from the project root (`chapters/...`), regardless of which file contains the `\input` command.
- To rearrange chapters, change only the order of the lines in `main.tex`; to rearrange subsections, change only the order in the chapter's `index.tex`.

## Managing references with Zotero

References are managed in Zotero and exported to `sources/lib.bib`. The export is kept up to date automatically, so you only change your library in Zotero and never edit the `.bib` file by hand.

### 1. Install Zotero

Download and install Zotero 7 or newer from <https://www.zotero.org/download/>.
I highly recommend to use the current stable version of Zotero.

### 2. Install the plugins

Plugins for Zotero are distributed as `.xpi` files on the GitHub release pages of the projects. Do not unpack the file.

| Plugin | Purpose | Download |
| --- | --- | --- |
| Better BibTeX | Stable citation keys and export to BibLaTeX (required) | <https://github.com/retorquere/zotero-better-bibtex/releases/latest> |
| Better Notes | Improved note taking inside Zotero (optional) | <https://github.com/windingwind/zotero-better-notes/releases/latest> |

Installation (the same for both plugins):

1. Download the latest `.xpi` file from the release page (under *Assets*). In some browsers you have to right-click the link and choose *Save link as*, otherwise the browser tries to install it itself.
2. In Zotero open *Tools, Plugins*.
3. Click the gear icon in the top right corner and choose *Install Plugin From File...*.
4. Select the downloaded `.xpi` file and restart Zotero if asked.

Further installation notes for Better BibTeX: <https://retorquere.github.io/zotero-better-bibtex/installation/>

### 3. Set up your library

1. Create a collection for your paper (right-click *My Library*, *New Collection...*).
2. Add your sources, for example with the browser connector of Zotero, by identifier (DOI, ISBN) or manually.
3. Check that each entry has the correct item type (book, journal article, book section, ...) and complete data. The quality of your bibliography depends directly on the quality of these entries.
4. Better BibTeX assigns a citation key to every entry (for example `mustermann2024`). You can see and change the key format in the Zotero settings under *Better BibTeX*.

### 4. Export to LaTeX

1. Right-click your collection and choose *Export Collection...*.
2. As format choose **Better BibLaTeX**.
3. Tick **Keep updated**, so that changes in Zotero are written to the file automatically.
4. Save the file as `sources/lib.bib` in this repository (replace the example file).

### 5. Cite in your text

Copy the citation key of an entry and use it in your text with the citation commands of the selected style, for example `\autocite{mustermann2024}` or `\cite{mustermann2024}`. The available commands are documented in the style files in `styles/`.

In the Zotero settings (*Export*, *Quick Copy*) you can choose a Better BibTeX format, so that *Ctrl+Shift+C* (macOS: *Cmd+Shift+C*) on a selected entry copies a ready-made citation command.

### 6. Citation style and bibliography structure (history)

The style `history_vechta` (in `styles/history/`) implements the Leitfaden für wissenschaftliches Arbeiten in der Geschichtswissenschaft an der Universität Vechta (version January 2026). It is loaded in `main.tex` with `style=history_vechta`. Places where the Leitfaden is inconsistent are marked with `RÜCKFRAGE DEKANAT` in the style files.

**Footnotes.** The first citation of a work is already a short citation (`Pollak, Identität, S. 169.`), as required by the Leitfaden. Repeated citations become `Ebd.`; `\autocite[Vgl.][26-28]{key}` gives `Vgl. ...`.

**Short title (required).** Every entry needs a short title, otherwise the full title is used and the compiler prints a warning. In Zotero fill the field **Short Title** (one or two meaningful nouns, for example `Identität`). Better BibTeX exports it as `shorttitle`.

**Short author for ancient sources (optional).** For ancient authors cited according to the abbreviations of *Der Neue Pauly* (DNP) leave *Short Title* empty and set the author abbreviation instead. In Zotero put this line into the **Extra** field:

```
tex.shortauthor: Ambr.
```

Work and passage then go into the optional argument: `\autocite[\stelle{paenit. 34}]{ambr}` gives `Ambr. paenit. 34.` (no `S.`; the abbreviations of authors and works are taken from the DNP list of abbreviations, they are not generated automatically).

**Splitting the bibliography.** `\printhistorybibliography` prints *Quellen* (ungedruckte, gedruckte), *Literatur* and *Bildquellen* as separate sections; empty sections are omitted. The assignment is done with Zotero tags, which Better BibTeX exports as `keywords`:

| Zotero tag | Section |
| --- | --- |
| `quelle-ungedruckt` | Quellen, Ungedruckte Quellen (archival material) |
| `quelle-gedruckt` | Quellen, Gedruckte Quellen (editions, source collections) |
| `bildquelle` | Bildquellen |
| *(no tag)* | Literatur |

If you only use `\nocite{*}`, call `\histAlleAbschnitte` before `\printhistorybibliography`. Headings can be changed with `\renewcommand{\histTitelLiteratur}{...}` (and `\histTitelQuellen`, `\histTitelUngedruckt`, `\histTitelGedruckt`, `\histTitelBilder`).

**Entry types.** Use the matching Zotero item type: book, book section (Aufsatz im Sammelband), journal article, newspaper article, encyclopedia article (Lexikonartikel), thesis, web page, blog post, manuscript (archival material), artwork (image source). Details and the fields that are evaluated are documented at the top of `styles/history/history_vechta.bbx`.

**Helpers for the text.** `\kuerzung` gives `[...]`, `\sic` gives `[sic!]`, `\ergaenzung{text}` gives `[text]`, and `\kinachweis{Tool}{Provider}{Prompt}{Date}{URL}` creates the footnote documenting the use of AI tools.

## License

This project is released under the [MIT License](LICENSE). The logos in `images/logos/vechta/` and the text of the declaration of independent work belong to the University of Vechta and are not covered by this license.
