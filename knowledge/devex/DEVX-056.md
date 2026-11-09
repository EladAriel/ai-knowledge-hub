# DEVX-056: PreToolUse recursive-delete guard: block unquoted rm -rf $VAR and repo-root deletes even in bypassPermissions (community hook)

## Summary

Add a PreToolUse recursive-delete guard so unquoted rm -rf $VAR / repo-root deletes are blocked even in bypassPermissions (community hook; upstream 107271 still open) - urlsextra: ["https://github.com/anthropics/claude-code/issues/107271"] - whatchanged: Repo created Nov 4 at 17:44Z (19:44 Israel time), MIT, stdlib Python only.

## Details

Repo created Nov 4 (19:44 Israel time), stdlib Python only, 8 stars, 34 self-tests, CI on Ubuntu and macOS. Motivating bug anthropics/claude-code#107271 (still open): zsh vs bash word-splitting turned a path with spaces into multiple operands including the repo root and .git, with no prompt under bypass mode. Exit code 2 reports the reason to Claude; works in every permission mode including bypassPermissions. Install: one curl + python3 /tmp/rdg.py --install copies the hook to ~/.claude/hooks, runs the self-test, backs up settings.json and adds a PreToolUse matcher for Bash|Write|Edit|MultiEdit; restart sessions afterwards. Success metric: self-test passes; a deliberate unquoted rm -rf $VAR probe is blocked in bypassPermissions. Caveats: lexical check only (does not follow eval/xargs); intentional deletes of protected paths must be done by a human; not an Anthropic fix. Pair with "onFailure": "block" on the hook so a missing script cannot fail open. Enterprise feasibility High, stage Trial, seen in 2 sources.

## Content

**[Add a PreToolUse recursive-delete guard so unquoted rm -rf $VAR / repo-root deletes are blocked even in bypassPermissions (community hook; upstream #107271 still open)](https://github.com/mishoko/claude-code-recursive-delete-guard)**
- **urls_extra:** ["https://github.com/anthropics/claude-code/issues/107271"]
- **what_changed:** Repo created Nov 4 at 17:44Z (19:44 Israel time), MIT, stdlib Python only. Motivated by anthropics/claude-code#107271 (opened Nov 4 18:02Z): an agent-written helper ran unquoted rm -rf $D; zsh (macOS Bash tool login shell) vs bash word-splitting turned a path containing spaces into multiple operands including the repo root and .git, with no prompt under bypass mode. The hook blocks unquoted $VAR/$(…) recursive deletes, find -delete/-exec rm with dynamic starts, deletes of /, ~, cwd, parents, git work-tree roots and .git, and the same patterns inside scripts the agent writes or runs. Exit code 2 reports the reason to Claude. Works in every permission mode including bypassPermissions. 8 stars at check time; 34 self-tests; CI on Ubuntu and macOS.
- **how_it_works:** One curl|python --install copies the hook to ~/.claude/hooks, runs the self-test, backs up settings.json and adds a PreToolUse matcher for Bash|Write|Edit|MultiEdit. Restart sessions afterwards.
- **enterprise_feasibility:** High
- **stage:** Trial
- **effort_minutes:** 10
- **poc_snippet:** # install command from the repo README (verbatim pattern)
curl -fsSL https://raw.githubusercontent.com/mishoko/claude-code-recursive-delete-guard/main/recursive_delete_guard.py -o /tmp/rdg.py \
  && python3 /tmp/rdg.py --install
# smoke: ask Claude to run  true || rm -rf /tmp/probe-$$
# expect: Blocked by recursive_delete_guard
# manual settings.json entry (from README):
# { "matcher": "Bash|Write|Edit|MultiEdit",
#   "hooks": [{ "type": "command",
#     "command": "python3 -I \"$HOME/.claude/hooks/recursive_delete_guard.py\"",
#     "timeout": 10 }] }
- **success_metric:** Self-test passes; a deliberate unquoted rm -rf $VAR probe is blocked in bypassPermissions; no silent repo-root deletes.
- **org_challenge_if_relevant:** Community hook (8 stars). Lexical check only — does not follow eval/xargs. Pair with onFailure: block (mod below) so a missing hook script cannot fail open. Intentional deletes of protected paths must be done by a human.
- **project_health_if_relevant:** New MIT repo with self-test + CI; links a same-day upstream bug. Not an Anthropic fix.
- **source_count:** 2
- **benefit_to_effort:** High
- **why_enterprise_simple:** One install command closes a real repo-wipe failure class that permission rules miss when the rm sits inside an agent-written script.

## Sources

- [recursive-delete-guard repo](https://github.com/mishoko/claude-code-recursive-delete-guard)
- [claude-code #107271](https://github.com/anthropics/claude-code/issues/107271)