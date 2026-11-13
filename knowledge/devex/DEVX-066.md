# DEVX-066: Collapse agent-written PR bodies behind \<details> (template, /pr-body command, Cursor rule)

## Summary

Reviewers see a short human-checked summary first; the full agent write-up sits in a collapsed \<details> block whose summary names the model and effort (Simon Willison's pattern). Feasibility High, stage Adopt, ~5 min.

## Details

PoC .github/pull_request_template.md: a 2-4 sentence human-checked comment, then \<details>\<summary>Agent notes (model + effort, e.g. Claude Opus, medium)\</summary> with the full agent description inside.
Success metric: time to first review; fewer 'too long, didn't read' review comments.
Merged ready-to-use mods: /pr-body slash command for Claude Code (.claude/commands/pr-body.md, ~3 min: top at most 3 plain sentences marked 'DRAFT: human to edit', everything else in Agent notes details, print Markdown only, don't open or edit the PR) and a Cursor rule .cursor/rules/pr-descriptions.mdc (~2 min: open with at most 3 sentences, rest in details, never claim tests passed unless run in this session). Full snippets below. Expires Feb 7, 2027.

## Content

### Collapse agent-written PR bodies behind `<details>` — Enterprise feasibility: High | Stage: Adopt
- What changes: reviewers see a short, human-approved summary first; the full agent write-up stays one click away, labeled with the model that wrote it.
- How it works: GitHub Markdown renders `<details><summary>` as a collapsed section. Simon Willison now puts a short human opener on top and the agent's essay inside a block whose summary names the model and effort.
- Effort: ~5 min (one rule line plus a PR template).
- PoC: add to `.github/pull_request_template.md`
```markdown
<!-- 2-4 sentences, human-checked: what this PR does and why it matters -->

<details>
<summary>Agent notes (model + effort, e.g. Claude Opus, medium)</summary>

<!-- full agent-written description goes here -->
</details>
```
- Success metric: time to first review, and fewer "too long, didn't read" review comments.
- Sources: [Simon Willison: Hide your slop PR descriptions](https://simonwillison.net/2026/Nov/9/details-summary/) | seen in 1 source | expires Feb 7, 2027

**Ready-to-use mods (Claude Code / Cursor)**

- [/pr-body slash command (Claude Code)](https://simonwillison.net/2026/Nov/9/details-summary/): drafts a PR body in the collapsed-details style, with a human opener left for you to edit. ~3 min. Save as `.claude/commands/pr-body.md`:
```markdown
---
description: Draft a PR body with a short human summary and collapsed agent notes
---
Write a PR description for the current branch vs main.
1. Top: at most 3 sentences, plain language: what changed and why. Mark it "DRAFT: human to edit".
2. Then wrap everything else (design, steps, tests run, risks) in:
<details>
<summary>Agent notes ({model name}, {effort})</summary>
...
</details>
Do not open or edit the PR; print the Markdown only.
```
- [Cursor rule: collapsed PR descriptions](https://simonwillison.net/2026/Nov/9/details-summary/): the same convention for Cursor's agent. ~2 min. Save as `.cursor/rules/pr-descriptions.mdc`:
```markdown
---
description: When writing pull request descriptions
alwaysApply: false
---
- Open with at most 3 plain sentences a reviewer can read in 10 seconds.
- Put all other detail inside <details><summary>Agent notes (model, effort)</summary> ... </details>.
- Never claim tests passed unless you ran them in this session.
```
Credit: pattern from Simon Willison; the snippets above are an adaptation of it.

## Sources

- [Simon Willison: Hide your slop PR descriptions](https://simonwillison.net/2026/Nov/9/details-summary/)
