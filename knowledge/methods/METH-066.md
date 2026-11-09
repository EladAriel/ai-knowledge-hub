# METH-066: GitHub Copilot Memory GA + 'dreaming' with PR-gated rule changes

## Summary

Dreaming reviews past sessions and updates memories freely, but changes to checked-in skills/instruction files come as PRs for human review.

## Details

GitHub numbers (no baseline): 93% of preview CLI sessions with memory followed preferences better, 42% more efficient workflows. Let memory self-update but route shared-rule changes through PR review; keep conventions in versioned files; track how often users repeat an instruction.

## Content

**1. [GitHub intelligence: Copilot Memory is generally available, plus "dreaming"](https://github.blog/changelog/2026-10-28-github-intelligence-puts-your-code-context-and-history-to-work/)** (Oct 28)
- **What shipped:** GitHub now has a context layer built from your repos, history and conventions.
  - Memory is available on paid plans.
  - Dreaming, in preview, reviews past sessions and updates memories.
- **The design choice to copy:** dreaming can edit memories freely, but any change to checked-in skills or instruction files comes as a pull request for a human to review.
- **GitHub's numbers:** in preview command-line sessions that used memory, 93% followed developer preferences better and 42% had more efficient workflows. These are GitHub's own numbers, with no comparison baseline published.
- Adopt for:
  - *Architects:* let memory update itself, but send changes to shared rules through pull request review.
  - *Product:* track how often users have to repeat an instruction. That's the number memory should bring down.
  - *Devs:* keep team conventions in versioned files, not in prompts.

## Sources

- [GitHub changelog](https://github.blog/changelog/2026-10-28-github-intelligence-puts-your-code-context-and-history-to-work/)