---
name: github-attribution
description: Convention for attributing GitHub content to the agent that authored it. Use whenever posting a comment to GitHub or filing an issue---via `gh issue comment`, `gh pr comment`, `gh pr review`, `gh issue create`, `gh api`, or similar---even if the user doesn't explicitly ask for attribution.
---

# GitHub attribution

When posting to GitHub (issue comments, PR comments, PR reviews, issue bodies), lead the body with an attribution line naming the agent, so readers can tell agent-authored content apart from the user's own. The GitHub author field shows the user's account even when the agent wrote it, so the line is the only signal.

## Format

```md
*From **Claude Code***

Body text here.
```

This does not apply to commit messages or pull request descriptions---those are already attributed via the `Co-Authored-By` trailer and the generated-with footer, respectively.
