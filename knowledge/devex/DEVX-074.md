# DEVX-074: A SessionStart hook that makes Claude Code skills actually fire (15% to 62% in a 2,808-run test)

## Summary

In a 2,808-run test on Claude Code 2.1.316, skills fired on reworded requests only 15% of the time; 'pushier' descriptions added ~5 points; a SessionStart hook telling Claude to check its skills first raised it to 62% (Sonnet 19% to 92%, Haiku 0% to 42%). Requests that only looked related never fired a skill. Feasibility High, stage Trial, ~5 min.

## Details

How it works: whatever a SessionStart hook prints goes into Claude's context. Caveats: the hook run was exploratory (designed after seeing the main results), Opus gained less, and it adds a few tokens to every session.
PoC (`.claude/settings.json`): a SessionStart command hook that echoes 'Before answering, asking a question, or reading code: check the available skills. If one could apply, invoke it first.' (full snippet below).
Success metric: share of sessions where your team's skills (review, testing, migration) load on the first tool call; check with 10 reworded prompts before and after. Seen in 3 sources. Expires Feb 9, 2027.

## Content

### 1. A SessionStart hook that makes your skills actually fire — Enterprise feasibility: High | Stage: Trial
- What changed: in a 2,808-run test on Claude Code 2.1.316, skills fired on reworded requests only 15% of the time. Making the skill descriptions "pushier" added about 5 points. A session-start hook telling Claude to check its skills first raised it to 62% (Sonnet went from 19% to 92%, Haiku from 0% to 42%). Requests that only looked related never fired a skill, in any setup.
- How it works: whatever a `SessionStart` hook prints goes into Claude's context. Caveats: the hook run was exploratory (designed after seeing the main results), Opus gained less, and it adds a few tokens to every session.
- Effort: ~5 min.
- PoC: add to `.claude/settings.json`:
  ```json
  { "hooks": { "SessionStart": [ { "hooks": [ { "type": "command",
    "command": "echo 'Before answering, asking a question, or reading code: check the available skills. If one could apply, invoke it first.'" } ] } ] } }
  ```
- Success metric: share of sessions where your team's skills (review, testing, migration) load on the first tool call. Check with 10 reworded prompts before and after.
- Sources: [Towards Data Science study](https://towardsdatascience.com/a-session-start-hook-raised-claude-code-skill-firing-from-15-to-62/), [TLDR summary](https://tldr.tech/story/13b07889-0575-4546-9fa5-01d57560cab0), [hooks guide (SessionStart stdout goes into context)](https://code.claude.com/docs/en/hooks-guide) | seen in 3 sources | expires Feb 9, 2027

## Sources

- [Towards Data Science study](https://towardsdatascience.com/a-session-start-hook-raised-claude-code-skill-firing-from-15-to-62/)
- [TLDR summary](https://tldr.tech/story/13b07889-0575-4546-9fa5-01d57560cab0)
- [hooks guide](https://code.claude.com/docs/en/hooks-guide)
