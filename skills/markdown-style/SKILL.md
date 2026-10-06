---
name: markdown-style
description: Conventions for writing Markdown---table formatting, smartypants shorthand for dashes, quotes, and ellipses, and sparing use of code spans. Use whenever writing or editing Markdown (SKILL.md files, READMEs, issues, PR descriptions, docs).
---

# Markdown style

## Tables

Use pipe tables without leading or trailing pipes. Pad each column to the width of its longest cell so the source stays readable unrendered, and make the header separator row match that width.

Example:

Prefer         | Over
-------------- | ----
No outer pipes | Outer pipes (`| a | b |`)
Padded columns | Cramped, unaligned columns

## Smartypants notation

Write the ASCII shorthand and let a smartypants-aware renderer (or the reader) turn it into the typographic character---don't hand-type the Unicode character directly.

Type       | Renders as
---------- | ----------
`--`       | en dash (–)
`---`      | em dash (—)
`...`      | ellipsis (…)
`'` / `"`  | curly quotes (' ' " ") where used as an actual quote/apostrophe

This applies in prose and inside table cells alike. It does not apply inside code spans/fences or the middle of identifiers---only in running text.

## Code spans

Use backtick code spans sparingly; they're visually heavy. For example, use them only on the first occurrence, only when the content is highly relevant, or only when it would otherwise be ambiguous whether the text refers to code.
