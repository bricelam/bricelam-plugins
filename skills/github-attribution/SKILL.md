---
name: github-attribution
description: Convention for attributing GitHub comments to the agent that posted them. Use whenever posting a comment to GitHub---via `gh issue comment`, `gh pr comment`, `gh pr review`, `gh api` comment endpoints, or similar---even if the user doesn't explicitly ask for attribution.
---

# GitHub attribution

When posting a comment to GitHub (issue comments, PR comments, PR reviews), lead the comment body with an attribution line naming the agent, so readers can tell agent-authored comments apart from the user's own.

## Format

```md
*From **Claude Code***

Comment text here.
```

This applies to comments posted directly by the agent. It does not apply to commit messages, PR descriptions, or issue bodies---those are already attributed via the git/GitHub author field.
