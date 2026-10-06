---
name: git-branch-naming
description: Convention for naming git branches locally versus on the remote. Use whenever creating a branch or pushing a branch to a remote.
---

# Git branch naming

Local branch names have no user prefix. Remote branch names are prefixed with `bricelam/`. Map between them when pushing:

```cmd
git push -u origin my-branch:bricelam/my-branch
```

Always name both sides of the refspec on a branch's first push. The user sets `push.default=upstream`, and branches created from remote-tracking refs (e.g. `git switch -c my-branch origin/main`) inherit that ref as their upstream, so a bare push would target the wrong remote branch (e.g. `main`).
