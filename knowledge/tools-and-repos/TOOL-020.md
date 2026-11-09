# TOOL-020: worktree-cleaner skill

## Summary

Lists your worktrees read-only and labels each one SAFE, AT_RISK, and so on (MIT, davila7/claude-code-templates).

## Details

It catches uncommitted work and ignored '.env' files that 'git worktree remove' would delete silently, and asks before each removal.

## Sources

- [worktree-cleaner](https://github.com/davila7/claude-code-templates/pull/1239)
