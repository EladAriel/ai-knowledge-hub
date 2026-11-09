# TOOL-020: worktree-cleaner skill

## Summary

Lists your worktrees read-only and labels each one SAFE, AT_RISK, and so on (MIT, davila7/claude-code-templates).

## Content

**[worktree-cleaner skill](https://github.com/davila7/claude-code-templates/pull/1239)** (~5 min, MIT, from davila7/claude-code-templates)
- It lists your worktrees read-only and labels each one SAFE, AT_RISK, and so on.
- It catches uncommitted work and ignored `.env` files that `git worktree remove` would delete silently, and asks before each removal.
```
npx claude-code-templates --skill git/worktree-cleaner
# then: "clean up my worktrees"
```

## Sources

- [worktree-cleaner](https://github.com/davila7/claude-code-templates/pull/1239)
