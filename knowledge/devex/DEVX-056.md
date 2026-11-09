# DEVX-056: PreToolUse recursive-delete guard: block unquoted rm -rf $VAR and repo-root deletes even in bypassPermissions (community hook)

## Summary

Community Claude Code hook (mishoko/claude-code-recursive-delete-guard, MIT) that blocks unquoted $VAR / $(…) recursive deletes, find -delete, and deletes of /, ~, cwd, parents, git roots and.git, including inside scripts the agent writes. Built after claude-code#107271, where an unquoted rm -rf $VAR wiped a repo root in bypass mode.

## Details

Repo created Nov 4 (19:44 Israel time), stdlib Python only, 8 stars, 34 self-tests, CI on Ubuntu and macOS. Motivating bug anthropics/claude-code#107271 (still open): zsh vs bash word-splitting turned a path with spaces into multiple operands including the repo root and .git, with no prompt under bypass mode. Exit code 2 reports the reason to Claude; works in every permission mode including bypassPermissions. Install: one curl + python3 /tmp/rdg.py --install copies the hook to ~/.claude/hooks, runs the self-test, backs up settings.json and adds a PreToolUse matcher for Bash|Write|Edit|MultiEdit; restart sessions afterwards. Success metric: self-test passes; a deliberate unquoted rm -rf $VAR probe is blocked in bypassPermissions.

## Sources

- [recursive-delete-guard repo](https://github.com/mishoko/claude-code-recursive-delete-guard)
- [claude-code #107271](https://github.com/anthropics/claude-code/issues/107271)
