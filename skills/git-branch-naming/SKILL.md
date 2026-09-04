---
name: git-branch-naming
description: Convention for naming git branches locally versus on the remote. Use whenever creating a branch or pushing a branch to a remote---even if the user doesn't explicitly ask for "branch naming" or "conventions."
---

# Git branch naming

Local branch names shouldn't include a reference to the user. Remote branch names should be prefixed with `<user>/`.

## Format

When pushing, map the local branch name to a `<user>/`-prefixed remote branch name.

```cmd
git push -u origin my-branch:bricelam/my-branch
```
