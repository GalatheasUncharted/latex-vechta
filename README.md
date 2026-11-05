# latex-vechta

A LaTeX template for academic papers at the University of Vechta.

This repository provides a ready-to-use template for writing term papers, seminar papers and theses at the University of Vechta with LaTeX. It contains the complete page layout, starting with the cover page, as well as citation styles that are adapted to the requirements of the individual departments (for example History or English Studies).

> **Status:** work in progress. The structure described below is the target layout; not all parts are available yet.

## Features

- Modular setup: `main.tex` only loads packages and global settings and then imports every part of the paper (cover page, chapters, declaration of independent work).
- Separate cover page (`cover/cover.tex`) that can be edited without touching the rest of the document.
- Department-specific citation styles for `biblatex`, selectable with a single line in `main.tex`.
- Example chapter and example declaration of independent work as a starting point.
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
│   ├── 00_examples/          Shipped examples (delete when you start)
│   │   ├── example_chapter.tex
│   │   └── doiw.tex          Declaration of independent work
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
│   │   └── vechta/           University logos
│   └── sign/                 Your own signature (image)
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

## License

This project is released under the [MIT License](LICENSE).
