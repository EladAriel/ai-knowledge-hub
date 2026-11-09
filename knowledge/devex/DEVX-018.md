# DEVX-018: Cursor Bugbot config + BUGBOT.md

## Summary

It reviews once per PR, skips drafts, and keeps autofix off. Rules are read from the base branch, and '.cursor/rules' doesn't apply to Bugbot. Credit: Cursor docs.

## Content

**[Cursor Bugbot config + BUGBOT.md](https://cursor.com/docs/bugbot)** is the Cursor version of the same review setup. It reviews once per PR, skips drafts, and keeps autofix off. Rules are read from the base branch, and `.cursor/rules` doesn't apply to Bugbot. Effort ~10 min. Credit: Cursor docs.
```yaml
# .cursor/config/bugbot.yaml
version: 1
triggers: { drafts: false, frequency: oncePerPr }
review: { effort: default, incremental: true }
autofix: { mode: disabled }
# .cursor/BUGBOT.md -> paste the REVIEW.md sections
```

## Sources

- [Cursor Bugbot docs](https://cursor.com/docs/bugbot)
