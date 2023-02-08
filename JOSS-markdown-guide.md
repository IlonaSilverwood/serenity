# Introduction

This article contains a general introduction to the popular markup language Markdown, as well as the
formatting requirements of Open Journals (OJ) and the Journal of Open Source Software (JOSS). 

## Markdown summary

Markdown is a lightweight markup language used frequently in software development and online
environments. Based on email conventions, it was developed in 2004 by John Gruber and Aaron Swartz. 

# Markdown primer

This section explains basic Markdown syntax. If you are already familiar with Markdown, the JOSS
formatting requirements can be found
[here](https://github.com/IlonaSilverwood/serenity/blob/main/JOSS-specific-guide.md).

## Inline markup

The markup in Markdown should be semantic, not presentations. The table below has some basic inline
markup and examples.

```
+---------------------+-------------------------+-----------------------+
| Markup              | Markdown example        | Rendered output       |
+:====================+:=======================:+:=====================:+
| emphasis            | `*this*`                | *this*                |
+---------------------+-------------------------+-----------------------+
| strong emphasis     | `**that**`              | **that**              |
+---------------------+-------------------------+-----------------------+
| strikeout           | `~~not this~~`          | ~~not this~~          |
+---------------------+-------------------------+-----------------------+
| subscript           | `H~2~O`                 | H~2~O                 |
+---------------------+-------------------------+-----------------------+
| superscript         | `Ca^2+^`                | Ca^2+^                |
+---------------------+-------------------------+-----------------------+
| underline           | `[underline]{.ul}`      | [underline]{.ul}      |
+---------------------+-------------------------+-----------------------+
| small caps          | `[Small Caps]{.sc}`     | [Small Caps]{.sc}     |
+---------------------+-------------------------+-----------------------+
| inline code         | `` `return 23` ``       | `return 23`           |
+---------------------+-------------------------+-----------------------+
```

### Links

Link syntax is `[link description](targetURL)`. E.g., this link to the [Journal of Open Source
Software](https://joss.theoj.org/) is written as \
`[Journal of Open Source Software](https://joss.theoj.org/)`.

Open Journal publications are not limited by the constraints of print publications. We encourage
authors to use hyperlinks for websites and other external resources. However, the standard
scientific practice of citing the relevant publications should be followed regardless.

### Grid Tables

Grid tables are made up of special characters which form the rows and columns, and also change table
and style variables.

Complex information can be conveyed by using the following features not found in other table styles:

* spanning columns
* adding footers
* using intra-cellular body elements
* creating multi-row headers

Grid table syntax uses the characters "-", "=", "|", and "+" to represent the
table outline:

* Hyphens (-) separate horizontal rows.
* Equals signs (=) produce a header when used to create the row under the header text.
* Equals signs (=) create a footer when used to enclose the last row of the table.
* Vertical bars (|) separate columns and also adjusts the depth of a row. 
* Plus signs (+) indicates a juncture between horizontal and parallel lines.

Note: Inserting a colon (:) at the boundaries of the separator line after the header will change
text alignment. If there is no header, insert colons into the top line.

Sample grid table:

```
+-------------------+------------+----------+----------+
| Header 1          | Header 2   | Header 3 | Header 4 |
|                   |            |          |          |
+:=================:+:==========:+:========:+:========:+
| row 1, column 1   | column 2   | column 3 | column 4 |
+-------------------+------------+----------+----------+
| row 2             | cells span columns               |
+-------------------+------------+---------------------+
| row 3             | cells      | - body              |
+-------------------+ span rows  | - elements          |
| row 4             |            | - here              |
+===================+============+=====================+
| Footer                                               |
+===================+============+=====================+
```

### Figures

To create a figure, a captioned image must appear by itself in a paragraph. The Markdown syntax for
a figure is a link, preceded by an exclamation point (!) and a description.

Example:

```markdown
![This description will be the figure caption](path/to/image.png)
```

```
![The "Mandrill" standard test image, sometimes erroneously called "Baboon", is a popular sample
photo and used in image processing research.](mandrill.jpg)
```

In order to create a figure rather than an image, there must be a description included and the
figure syntax must be the only element in the paragraph, i.e., it must be surrounded by blank lines.

Images that are larger than the text area are scaled to fit the page. You can give images an
explicit height and/or width, e.g. when adding an image as part of a paragraph. The Markdown `![Nyan
cat](nyan-cat.png){height="9pt"}` includes the image "nyan-cat.png" Nyan cat{height="9pt"} while
scaling it to a height of 9 pt.

### Citations

Bibliographic data should be collected in a `.bib` file; while BibLaTex is preferred, plain BibTeX
is also acceptable. All major citation managers offer to export these formats.

Cite a bibliography entry by referencing its identifier: `[@upper1974]` will create the reference
"(Upper et al, 1974)". Omit the brackets when referring to the author as part of a sentence: "For a
case study on writers block, see @upper1974." Please refer to the [pandoc
manual](https://pandoc.org/MANUAL#extension-citations) for additional features, including page
locators, prefixes, suffixes, and suppression of author names in citations.

### Mathematical Formulæ

Mark equations and other math content with dollar signs (`$`). Use a single dollar sign (`$`) for
math that will appear directly within the text. Use two dollar signs (`$$`) when the formula is to
be presented centered and on a separate line, in "display" style. The formula itself must be given
using TeX syntax.

To give some examples: When discussing a variable $x$ or a short formula like $\sin \frac{\pi}{2}$,
we would write `$x$` and `$\sin \frac{\pi}{2}$`, respectively. However, for more complex formulæ,
display style is more appropriate. Writing `$$\int_{-\infty}^{+\infty} e^{-x^2} \, dx =
\sqrt{\pi}$$` will give us

$$\int_{-\infty}^{+\infty} e^{-x^2} \, dx = \sqrt{\pi}$$

Numbered equations and internal cross-references are discussed [further below][Equations].

### Footnotes

Syntax for footnotes centers around the "caret" character `^`. The symbol is also used as a
delimiter for superscript text and thereby mirrors the superscript numbers used to mark a footnote
in the final text.[^markers]

``` markdown
Articles are published under a Creative Commons license[^1].
Software should use an OSI-approved license.

[^1]: An open license that allows reuse.
```

The above example results in the following output:

> Articles are published under a Creative Commons license[^1]. Software should use an OSI-approved
> license.
>
> [^1]: An open license that allows reuse.

Note: numbers do not have to be sequential, they will be reordered automatically in the publishing
step. In fact, the identifier of a note can be any sequence of characters, like `[^marker]`, but may
not contain whitespace characters.

[^markers]: it should be noted that some publishers prefer symbols or letters as footnote markers.

## Blocks

The larger components of a document are called "blocks".

### Headings

Headings are added with `#` followed by a space, where each additional `#` demotes the heading to a
level lower in the hierarchy:

```markdown
# Section

## Subsection

### Subsubsection
```

Please start headings on the first level. The maximum supported level is 5, but paper authors are
encouraged to limit themselves to headings of the first two or three levels.

#### Deeper nesting

Fourth- and fifth-level subsections – like this one and the following heading – are supported by the
system; however, their use is discouraged.

##### Avoiding excessive nesting

Usually [lists], as described in the next section, should be preferred over forth- and fifth-level
headings.


### Lists

Bullet lists and numbered lists, a.k.a. enumerations, offer an additional method to present
sequential and hierarchical information.

``` markdown
- apples
- citrus fruits
  - lemons
  - oranges
```

- apples
- citrus fruits
  - lemons
  - oranges

Enumerations start with the number of the first item. Using the the first two [laws of
thermodynamics](https://en.wikipedia.org/wiki/Laws_of_thermodynamics) as example.

``` markdown
0. If two systems are each in thermal equilibrium with a third, they are
   also in thermal equilibrium with each other.
1. In a process without transfer of matter, the change in internal
   energy, $\Delta U$, of a thermodynamic system is equal to the energy
   gained as heat, $Q$, less the thermodynamic work, $W$, done by the
   system on its surroundings. $$\Delta U = Q - W$$
```

Rendered:

0. If two systems are each in thermal equilibrium with a third, they are also in thermal equilibrium
   with each other.
1. In a process without transfer of matter, the change in internal energy, $\Delta U$, of a
   thermodynamic system is equal to the energy gained as heat, $Q$, less the thermodynamic work,
   $W$, done by the system on its surroundings. $$\Delta U = Q - W$$
