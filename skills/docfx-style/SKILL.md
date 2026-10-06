---
name: docfx-style
description: Conventions for DocFX documentation---`toc.yml` table-of-contents structure. Use whenever creating or editing a DocFX `toc.yml` or documentation site navigation.
---

# DocFX style

## TOC entries

If a TOC entry has child items, don't specify `href` on it. Instead, use the first child item to represent the parent.

```yaml
# Good
- name: Functions
  items:
  - name: Overview
    href: functions/index.md
  - name: Math
    href: functions/math.md

# Bad
- name: Functions
  href: functions/index.md
  items:
  - name: Math
    href: functions/math.md
```
