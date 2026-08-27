---
name: markdown-style
description: Conventions for writing Markdown---plain/simple table formatting (no outer pipes, columns aligned with padding) and smartypants shorthand for dashes, quotes, and ellipses. Use whenever writing or editing Markdown prose, tables, or documentation (SKILL.md files, READMEs, issues, PR descriptions, commit-adjacent docs)---even if the user doesn't explicitly ask for "formatting" or "style."
---

# Markdown style

Conventions for Markdown content. Apply these by default; only deviate if the user says otherwise or the file already has an established, different convention.

## Tables

Use the plain/simple table form---no leading or trailing pipes. Pad each column to the width of its longest cell so the source stays readable unrendered, and make the header separator row match that width.

Example:

Prefer         | Over
-------------- | ----
Plain tables   | Pipe-fenced tables (`| a | b |`)
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
