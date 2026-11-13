# DEVX-070: Use the 'you own this code' sentence only in a dedicated refactor subagent (Fable 5.2)

## Summary

One ownership sentence makes Fable 5.2 merge duplicated code instead of adding more (Anthropic: about 50% of tries vs under 10% without), but costs ~1.5x output tokens, adds unrequested changes and in 1 of 6-10 tries changes existing behavior. Keep it out of CLAUDE.md; use it only in a refactor agent. Feasibility High, stage Trial, ~5 min.

## Details

Why isolate it: a 'no drive-by refactors' rule elsewhere in the prompt doesn't cancel it; also check existing prompts don't already call the code 'yours'.
Mods: `.claude/agents/refactor-owner.md` (Claude Code subagent, description 'Use only when the user explicitly asks to refactor or consolidate duplicated code'; body: the ownership sentence, merge duplicates and fix closely related problems, don't change external behavior, run existing tests before and after, list every changed file and why). Cursor: `.cursor/rules/refactor-mode.mdc` with alwaysApply: false, applied only when @-mentioned. Full snippets below.
Success metric: duplicate-code findings closed per refactor PR, with no rise in tokens per normal task. Seen in 4 sources. Expires Feb 8, 2027.
AI methods review (Nov 10): effectiveness 3/5 · hype 2/5; recommendation Adopt as a check; the official guide includes a version-migration checklist; the closing summary skips small changes, so check the diff.

## Content

### 1. Turn on "you own this code" only in a refactor subagent — Enterprise feasibility: High | Stage: Trial
- What changes: one sentence makes Fable 5.2 merge duplicated code instead of piling on more. Anthropic's tests saw about 50% of tries with the sentence versus under 10% without it.
- How it works: the sentence also costs about 1.5x the output tokens. It adds changes nobody asked for, and in one try in six to ten it changes how an existing feature behaves. A "no drive-by refactors" rule elsewhere in the prompt doesn't cancel it. So keep it out of `CLAUDE.md` and use it only in a dedicated refactor agent, where a wide diff is what you want. Also check that your existing prompts don't already call the code "yours".
- Effort: ~5 min.
- PoC: see the `refactor-owner` subagent in the mods below.
- Success metric: duplicate-code findings closed per refactor PR, with no rise in tokens per normal task.
- Sources: [Anthropic: Prompting Claude Fable 5.2](https://platform.claude.com/docs/en/build-with-claude/prompt-engineering/prompting-claude-fable-5-2), [Simon Willison](https://simonwillison.net/2026/Nov/10/prompting-claude-fable-52/), [explainx write-up](https://explainx.ai/blog/claude-fable-5-2-code-ownership-prompting-guide-2026) | seen in 4 sources | expires Feb 8, 2027

**Ready-to-use mods (Claude Code / Cursor)**

- [refactor-owner subagent (Claude Code)](https://platform.claude.com/docs/en/build-with-claude/prompt-engineering/prompting-claude-fable-5-2): a refactor-only agent that uses Anthropic's ownership sentence, so your default sessions stay surgical. ~3 min. Save as `.claude/agents/refactor-owner.md`:
```markdown
---
name: refactor-owner
description: Use only when the user explicitly asks to refactor or consolidate duplicated code.
---
This codebase is yours: what it's for and how it's built are your call, and you'll keep building on it.
Merge duplicated code and fix closely related problems you find.
Do not change any feature's external behavior. Run the existing tests before and after.
End with a list of EVERY file you changed and why, including small changes.
```
- [Cursor rule: refactor mode](https://platform.claude.com/docs/en/build-with-claude/prompt-engineering/prompting-claude-fable-5-2): the same idea for Cursor. It only applies when you @-mention it. ~2 min. Save as `.cursor/rules/refactor-mode.mdc`:
```markdown
---
description: Refactor mode. Apply only when explicitly @-mentioned for a refactor task
alwaysApply: false
---
This codebase is yours: what it's for and how it's built are your call, and you'll keep building on it.
- Consolidate duplicated code; keep external behavior unchanged.
- List every changed file in the final message; never claim tests ran unless they did.
```

Credit: the ownership sentence is Anthropic's, and the files around it are an adaptation.

## Sources

- [Anthropic: Prompting Claude Fable 5.2](https://platform.claude.com/docs/en/build-with-claude/prompt-engineering/prompting-claude-fable-5-2)
- [Simon Willison](https://simonwillison.net/2026/Nov/10/prompting-claude-fable-52/)
- [explainx write-up](https://explainx.ai/blog/claude-fable-5-2-code-ownership-prompting-guide-2026)
