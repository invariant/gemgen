# gemgen - Markdown to Gemtext

Command line tool for converting [Commonmark Markdown](https://commonmark.org/)
to [Gemtext](https://gemini.circumlunar.space/docs/gemtext.gmi). Gemgen uses the
[goldmark](https://pkg.go.dev/github.com/yuin/goldmark) markdown parser and [my
gemtext rendering module](https://git.sr.ht/~kota/goldmark-gemtext/).

The goal is to create proper _hand-made_ gemtext. Links and "autolinks" are
placed below each paragraph, but a "paragraph" of **only** links is left intact.
Normally, paragraphs are merged onto a single line, but hardlinks (double spaces
or \ at the end of a line) may be used for manual line breaks. Lists and
headings are simplified to the gemtext format, emphasis markings are removed (or
kept with the `-e` flag), horizontal rules are turned into 80 character lines,
and indented code is converted to the gemtext "fenced" format.

## Usage

```
gemgen [-v] [-e] [-i input.md] [-o output.gmi]
 -v : Print version and exit.
 -e : Keep emphasis symbols for bold, italics, inline code, and strikethrough.
 -i : Read from a file instead of standard input.
 -o : Write to an output file instead of standard output.
```

## Build and Install

Build dependencies:  
 * golang
 * make
 * sed
 * scdoc

Optionally configure `config.mk` to specify a different install location.  
Defaults to `/usr/local/`

`sudo make all`

## Uninstall

`sudo make uninstall`

## Examples

### Paragraphs
```md
# Typeface

A typeface is the design of [lettering](https://en.wikipedia.org/wiki/Lettering)
that can include variations in size, weight (e.g. bold), slope (e.g. italic),
width (e.g. condensed), and so on. Each of these variations of the typeface is a
font. There are [thousands of different
typefaces](https://en.wikipedia.org/wiki/List_of_typefaces) in existence, with
new ones being developed constantly. The art and craft of designing typefaces is
called [_type design_](https://en.wikipedia.org/wiki/Type_design). Designers of typefaces are called [_type designers_](https://en.wikipedia.org/wiki/Type_designer) and are
often employed by [_type foundries_](https://en.wikipedia.org/wiki/Type_foundry). In digital typography, type designers are
sometimes also called _font developers_ or _font designers_.

## Popular Fonts

[DejaVu](https://dejavu-fonts.github.io/)\
[EB Garamond](https://github.com/octaviopardo/EBGaramond12)\
[Merriweather](https://fonts.google.com/specimen/Merriweather)\
[Minion](https://fonts.adobe.com/fonts/minion)\
[Palatino](https://en.wikipedia.org/wiki/Palatino)\
[PT Sans](https://en.wikipedia.org/wiki/PT_Fonts)
```
```gemtext
# Typeface

A typeface is the design of lettering that can include variations in size, weight (e.g. bold), slope (e.g. italic), width (e.g. condensed), and so on. Each of these variations of the typeface is a font. There are thousands of different typefaces in existence, with new ones being developed constantly. The art and craft of designing typefaces is called type design. Designers of typefaces are called type designers and are often employed by type foundries. In digital typography, type designers are sometimes also called font developers or font designers.

=> https://en.wikipedia.org/wiki/Lettering lettering
=> https://en.wikipedia.org/wiki/List_of_typefaces thousands of different typefaces
=> https://en.wikipedia.org/wiki/Type_design type design
=> https://en.wikipedia.org/wiki/Type_designer type designers
=> https://en.wikipedia.org/wiki/Type_foundry type foundries

## Popular Fonts

=> https://dejavu-fonts.github.io/ DejaVu
=> https://github.com/octaviopardo/EBGaramond12 EB Garamond
=> https://fonts.google.com/specimen/Merriweather Merriweather
=> https://fonts.adobe.com/fonts/minion Minion
=> https://en.wikipedia.org/wiki/Palatino Palatino
=> https://en.wikipedia.org/wiki/PT_Fonts PT Sans
```

### Qoutes
```md
> When education is not liberatory, the dream of the oppressed is to be the
> oppressor. - Paulo Freire
```
```gemtext
> When education is not liberatory, the dream of the oppressed is to be the oppressor. - Paulo Freire
```

### Linebreaks
```md
_A Farewell_ - Langston Hughes

With gypsies and sailors,\
Wanderers of the hills and seas,\
I go to seek my fortune.\
With pious folk and fair\
I must have a parting.\
But you will not miss me, —\
You who live between the hills\
And have never seen the seas.
```
```gemtext
A Farewell - Langston Hughes

With gypsies and sailors,
Wanderers of the hills and seas,
I go to seek my fortune.
With pious folk and fair
I must have a parting.
But you will not miss me, —
You who live between the hills
And have never seen the seas.
```

### Lists
```md
* item
* item
* item

- item
  - sub-item (two spaces)
  - sub-item
- item
- item

1. one
2. two
3. three
```
```gemtext
* item
* item
* item

* item
  * sub-item (two spaces)
  * sub-item
* item
* item

* one
* two
* three
```