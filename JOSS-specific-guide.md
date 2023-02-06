# Summary

This section describes the features of the Journal of Open Source Software
(JOSS) [[@smith2018]](https://peerj.com/articles/cs-147/) publishing pipeline. The publishing method uses Markdown as
the input format, which is similar to the model described by [@krewinkel2017](https://peerj.com/articles/cs-112/). The
files provided by the author serve as the source for all generated publishing
artifacts.

Submitted articles must provide a metadata section at the beginning of the
article, before the main text. Metadata must be formatted using [YAML](https://yaml.org), a
human-friendly data serialization language (The Official YAML Web Site, 2022).
This information is included in the title and sidebar of the subsequently
generated PDF.

Authors who face difficulties while writing are referred to the paper by
[@upper1974](https://onlinelibrary.wiley.com/doi/epdf/10.1901/jaba.1974.7-497a).


# Statement of Need

JOSS maintains a detailed and helpful
[article](https://joss.readthedocs.io/en/latest/submitting.html) on the
requirements articles must satisfy in order to be considered for publication.
However, the linked article does not provide guidance on using the lightweight
markup language *Markdown*, which is the required format for papers submitted to
JOSS.

This article explains the technical details and describes the publishing
system's capabilities. It can also be used as a test document, or serve as a
template that can be used as a starting point.

# Article metadata

## Names

Providing an author name is straightforward: just set the `name` attribute.
However, sometimes fine-grained control over the name is required.

### Name parts

There are many ways to describe the parts of names; we support the following:

- given names,
- surname,
- dropping particle,
- non-dropping particle,
- and suffix.

We use a heuristic to parse names into these components. This parsing may
produce the wrong result, in which case it is necessary to provide the relevant
parts explicitly.

The respective field names are

- `given-names` (aliases: `given`, `first`, `firstname`)
- `surname` (aliases: `family`)
- `suffix`

The full display name will be constructed from these parts, unless the `name`
attribute is given as well.

### Particles

It's usually enough to place particles like "van", "von", "della", etc. at the
end of the given name or at the beginning of the surname, depending on the
details of how the name is used.

- `dropping-particle`
- `non-dropping-particle`

### Literal names

The automatic construction of the full name from parts is geared towards common
Western names. It may therefore be necessary sometimes to provide the display
name explicitly. This is possible by setting the `literal` field, e.g.,
`literal: Tachibana Taki`. This feature should only be used as a last resort.
<!-- e.g., `literal: 宮水 三葉`. -->

#### Example

```yaml
authors:
  - name: John Doe

  - given-names: Ludwig
    dropping-particle: van
    surname: Beethoven

  # not recommended, but common aliases can be used for name parts.
  - given: Louis
    non-dropping-particle: de
    family: Broglie
```

The name parts can also be collected under the author's `name`:

``` yaml
authors:
  - name:
      given-names: Kari
      surname: Nordmann
```

  <!-- - name: -->
  <!--     literal: 立花 瀧 -->
  <!--     given-names: 瀧 -->
  <!--     surname: 立花 -->
  
## Joint authorship

Indicate joint first authors by setting the `equal-contrib` attribute.

``` yaml
- name: John Doe
  equal-contrib: true
- name: Janet Davison
  equal-contrib: true
```

## Corresponding author

Designate a corresponding author with the `corresponding` attribute.

```yaml
- name: John Doe
  corresponding: true
```
  
## Email

Include the author's email by setting the `email` attribute. 
``` yaml
- name: John Doe
  equal-contrib: true
  email: johndoe@ubc.ca
```

## Affiliations

Map the list of affiliation metadata values by including the `index` field with the `author`
metadata, then setting the `name` and `index` fields under the
`affiliations` attribute. 

``` yaml
- name: John Doe
  equal-contrib: true
  email: johndoe@ubc.ca
  index: 2
```

```yaml
affiliations:
 - name: Lyman Spitzer, Jr. Fellow, Princeton University, USA
   index: 1
 - name: Institution Name, Country
   index: 2
 - name: Independent Researcher, Country
   index: 3
```
Multiple affiliations must be enclosed in quotation marks. 

```yaml
- name: Jane Doe
  index: "1, 2"
```

# Internal references

The goal of [Open Journals](https://theoj.org) is to provide authors with a seamless and pleasant
writing experience. Since Markdown has no default mechanism to handle document
internal references, known as “cross-references”, Open Journals supports a
limited set of LaTex commands. In brief, elements that were marked with `\label`
and can be referenced with `\ref` and `\autoref`.

## Tables and figures

Tables and figures can be referenced if they are given a *label* in the caption.
In pure Markdown, this can be done by adding an empty span
`[]{label="floatlabel"}` to the caption. LaTeX syntax is supported as well:
`\label{floatlabel}`.

Link to a float element, i.e., a table or figure, with `\ref{identifier}` or
`\autoref{identifier}`, where `identifier` must be defined in the float's
caption. The former command results in just the float's number, while the latter
inserts the type and number of the referenced float. E.g., in this document
`\autoref{proglangs}` yields "\autoref{proglangs}", while `\ref{proglangs}`
gives "\ref{proglangs}".

: Comparison of programming languages used in the publishing tool.
  []{label="proglangs"}

| Language | Typing          | Garbage Collected | Evaluation | Created |
|----------|:---------------:|:-----------------:|------------|---------|
| Haskell  | static, strong  | yes               | non-strict | 1990    |
| Lua      | dynamic, strong | yes               | strict     | 1993    |
| C        | static, weak    | no                | strict     | 1972    |

## Equations

Cross-references to equations work similarly to those for floating elements. The
difference is that, since captions are not supported for equations, the label
must be included in the equation:

    $$a^n + b^n = c^n \label{fermat}$$

Referencing, however, is identical, with `\autoref{eq:fermat}` resulting in
"\autoref{eq:fermat}".

$$a^n + b^n = c^n \label{eq:fermat}$$

Authors who do not wish to include the label directly in the formula can use a
Markdown span to add the label:

    [$$a^n + b^n = c^n$$]{label="eq:fermat"}

# Behind the scenes

Readers may wonder about the reasons behind some of the choices made for paper
writing. Most often, the decisions were driven by radical pragmatism. For
example, Markdown is not only nearly ubiquitous in the realms of software, but
it can also be converted into many different output formats. The archiving
standard for scientific articles is JATS, and the most popular publishing format
is PDF. Open Journals has built its pipeline based on
[pandoc](https://pandoc.org), a universal document converter that can produce
both of these publishing formats as well as many more.

A common method for PDF generation is to go via LaTeX. However, support for
tagging -- a requirement for accessible PDFs -- is not readily available for
LaTeX. The current method used ConTeXt, to produce tagged PDF/A-3, a format
suited for archiving [@pdfa3](https://www.pdf-tools.com/en/resources/pdfa-archive-format/pdfa-3-overview/).

