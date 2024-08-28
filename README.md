# Harry Potter and the Methods Of Rationality

This is a XeLaTeX version of [the popular didactic fan-fiction](http://www.hpmor.com) by Eliezer Yudkowsky, which can make e-books, and six volumes in PDF that can be printed and bound. There are also dust jackets for the printable volumes.

See [latest release](https://github.com/JakubJanowski/hpmor/releases/latest) for PDF downloads.

The source for this version was originally taken from https://github.com/rrthomas/hpmor, then changes from https://github.com/xenohedron/hpmor-xetex were applied on top of it to aggregate the improvements made by fans on independent versions of this fiction. This repository also includes my individual changes.

## Features
- Includes an edited version of _Daystar's Remix of Rationality_ which improves the flow and tone of chapters 1-4
- Spellcheck and standardization
  - Fixed typos
  - Removed early Britpicks for consistent usage throughout
  - Removed Omake files and epigraphs from individual volumes
  - Standardization of formats for dates and times
  - Consistent capitalization of various words
  - Minor improvements to italics, lists, notes, and headlines
- LaTeX formatting code restructured, pruned, and somewhat commented
  - Separate .tex file for each chapter
  - Formatting and macros in common header
- Outputs six PDF files for printing the story in six volumes
  - Page size 9in. by 6in.
  - Bookmarks and unobtrusive links with hyperref
  - Automatic chapter numbering restarts in each subbook with ToC
- Careful typography
  - Text set in 12-point Alegreya, chapter headings set in Lumos
  - American English hyphenation rules
  - Large initial capitals at the start of each chapter with lettrine
  - Microtype protrusion
  - Adjusted line spacing
  - Nonbreaking spaces, hyphenation, en/em dashes and ellipses
  - Lumos font kerning 
  - Manual linebreaks in long chapter titles
  - Fancy headers, footers, and section breaks

## Files

- `hpmor.tex` - the main file.
- `hpmor-ebook.tex` - the ebook file.
- `layout/hp-format.tex` - mostly sets up memoir.
- `layout/hp-markup.tex` - logical markup commands used in the text.
- `chapters/` - one file per chapter, included from `hpmor.tex` and the individual volumes `hpmor-N.tex`.
- `spelling-list.txt` - a list of words used to spell-check the book.
- `fonts/` - various fonts used.
- `latexmkrc` - configures latexmk to run LaTeX to build the PDFs.

## Building the book(s)

TeXLive 2015 or later and git are required to build the book. (Note: the book must be built from a git checkout.)

Note: the Omake Files chapters (11 and 64) have been moved to the end of the single-file PDF. Those chapter numbers are omitted in the text, so chapter ,10 is followed by chapter 12, for example. In the six-volume PDFs, all chapters are renumbered to start from 1 at the start of a book, and there are no appendices. Some epigraphs have been omitted but are in the source files of the chapters.

### Extra packages required

- `hyphenex` providing `ushyphex.tex` file containing a list of exceptions for American English hyphenation patterns.

### Build commands

- `latexmk -xelatex`: Build all PDFs. (If in doubt, just run this command and do something else for twenty minutes!).
- `latexmk -xelatex hpmor`: Build the one-volume PDF `hpmor.pdf`.
- `latexmk -xelatex hpmor-ebook`: Build the ebook PDF `hpmor-ebook.pdf`.
- `latexmk -xelatex hpmor-N`: Build one of the six individual volumes `hpmor-1.pdf` to `hpmor-6.pdf`.
- `latexmk -xelatex layout/hpmor-dust-jacket-N`: produce the dust jacket for Volume N, `hpmor-dust-jacket-N.pdf`. Note that this requires the corresponding volume, `hpmor-N.pdf`, to have been built first.
- `latexmk -c`: Remove files produced by building (except PDFs).
- `latexmk -C`: Remove files produced by building (including PDFs).

By default, the dust jackets assume 80gsm plain paper (this affects the thickness of the book and hence the size of the dust jacket). This can be configured in `layout/hp-paper-type.tex`; see `layout/papers.tex` for a list of papers.

The exact sizes of dust jackets may vary; the current parameters were taken from a commercial printer. They can be adjusted in `hp-dust-jacket.tex` as desired.

Note that the back dust-flap is left for you to add your own text; edit `layout/hp-dust-jacket.tex` and search for “PUT YOUR BACK DUST-FLAP TEXT HERE!”. Make sure you remove the percent sign `%` at the start of the line, or your text will not be printed. This is a safety feature to make sure that if you don’t change the text, the placeholder will not appear; instead, you’ll just get a blank back flap.

To build a single chapter, from the `chapters` directory use the command:

`latexmk -norc -e '$chapter="N"' -r ../latexmkrc -g hpmor-chapter-NNN`

Similarly, to build a single appendix or other non-chapter section, from the top directory use the command:

`latexmk -norc -e '$chapterfile="FILENAME"' -r latexmkrc -g FILENAME`

## Contributing

Contributions are most welcome. These fall into the following categories:

1. Textual corrections (where the text differs from the online original unintentionally).
2. Textual improvements: fixing straight-up errors in the English (or deeper, the sense, story etc.), or replacing British usages with American/international ones.
3. Design and typography. Improvements to both the PDF and print versions of the books are encouraged. See the GitHub bug-tracker for known issues; also, search the sources for “FIXME”.

For textual changes other than simple typo or language fixes, please familiarize yourself with the style guide (below).

The preferred way to submit any improvement is as a GitHub pull request. Textual corrections can also be submitted as issues in the issue tracker.

## Style guide

### Spelling

When spell-checking, use `spelling-list.txt` instead of your personal dictionary, so the results are less dependent on your setup. (The system dictionary can still of course vary from one setup to another.)

Words that are standard English or part of the Harry Potter universe, or are otherwise of “global” relevance should be added to `spelling-list.txt`. Exclamations (“Eeeehhhh”) and other one-offs should be added to the per-file word lists. (There’s obviously something of a grey area in the middle, e.g. one-off references to various real and fictional people.)

### Chapter headings

Chapters that aren’t part of a continuing series look like this:

`\chapter{The Fundamental Attribution Error}`

Chapters that are part of a continuing series look like one of these:

`\partchapter{Working in Groups}{I}`

`\namedpartchapter{Self-Actualization}{SA}{VIII}{The Sacred and the Mundane}`

The first is pretty simple; it’s just the title of the chapter followed by which part it is.

The second looks like the title of the chapter, then the abbreviation for the title of the chapter, then the part, then the title of the part.

### First sentences

Normally, a chapter starts like this:

`\lettrine{P}{adma} Patil had finished`

That creates the large initial letter.

If the first paragraph of the chapter is all italics, though, it looks like this:

    \begin{em}\lettrine{T}{he} red jet of fire took Hannah full in the
    [...]
    blazing green spirals brought down their foe’s Shield Charm.\par\end{em}

### Sections

`\section{Final Aftermath:}`

### Miscellaneous

There are some other things relating to newspaper headlines and such; check the chapters they appear in for the appropriate markup.

### Markup

These are macros defined in `layout/hp-markup.tex`. You should glance through that file to see what commands are available, and use them instead of direct markup; for example `\shout` rather than `\textsc`.

<!--  LocalWords:  hpmor tex hp txt latexmkrc latexmk 80gsm norc NNN chapterfile
 -->
<!--  LocalWords:  Eeeehhhh partchapter namedpartchapter lettrine adma textsc
 -->
