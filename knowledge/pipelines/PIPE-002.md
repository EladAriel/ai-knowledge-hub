# PIPE-002: Claude Code team's layered code review

## Summary

Stack automated checks so humans spend attention only where risk is; merged PRs doubled while revert rate fell >40%.

## Details

Flow: change -> Claude runs tests/build/lint -> fresh-context subagent reviews diff -> required CI -> parallel AI bug hunters with verifier agents voting -> separate security review -> risk classifier sets 0/1/2 human approvals -> merge queue -> feature flag + staged release -> fast rollback. Findings tagged Important/Nit/Pre-existing; every thread fixed or resolved with a reason. Anti-loop: cap 3 rounds, re-review only new diff, flag bug class, never repeat findings (mean reviews to pass 2.08 -> 1.32). Past incidents/reverts become a daily reviewer eval. Example: REVIEW.md (failure definitions, skip generated, cite file:line, max 3 nits), CLAUDE.md with runnable checks, PR template with Testing/Risk/How to revert. Verdict: yes for pre-PR verification + REVIEW.md. DevEx (2026-10-18, Copy the Claude Code team's review recipe): - What changed: Anthropic's post (457 points on HN, also quoted by Simon Willison) says merged PRs more than doubled s check CLAUDE.md compliance, bugs and git-blame context, and only findings scored 80 or higher are kept. It now prints to the terminal by default. Credit: Anthropic, PR #6905. /plugin install code-review@claude-plugins-official /code-review # local, terminal output /code-review --comment # post to the PR

## Content

- When agents write most of the code, stop asking "did a human read every line" and stack automated checks so people only spend attention where the risk is. The trade-off is upfront setup and tuning, plus a noisy reviewer that can loop endlessly with an agent author.
- If agents open PRs on your React, Python, and TypeScript apps, human review becomes the bottleneck fast. The Claude Code team doubled merged PRs from June to September while the revert rate fell by more than 40 percent.

- The flow: change → Claude runs tests, build, and lint, then a fresh-context subagent reviews the diff → required CI → parallel AI bug hunters, with verifier agents voting on each finding → separate security review → a risk classifier sets zero, one, or two human approvals → merge queue → feature flag and staged release → fast rollback.
- Findings are tagged Important, Nit, or Pre-existing, and every thread must be fixed or resolved with a reason before merge.
- To stop agent-vs-agent loops, they cap review at three rounds, re-review only the new diff, flag the whole class of bug, and never repeat findings. That cut mean reviews to pass from 2.08 to 1.32.
- Past incidents and reverts become an eval set the reviewer runs against daily, so every prompt or model change has to beat it.

Example
- In a React + FastAPI RAG app, add a short `REVIEW.md`: "failure here means a hallucinated citation or a leaked API key; skip `web/src/generated/`; cite file and line as evidence; max 3 nits." Keep `CLAUDE.md` to the stack plus the checks Claude must run: `pnpm test`, `pnpm tsc --noEmit`, `pytest api/tests`.
- A prompt.submit hook appends "run the tests and paste the output before you say done" to every prompt, so verification happens before any review.
- Agent edits `api/routes/chat.py` and `web/src/components/ChatPanel.tsx` → runs `pytest` and `pnpm test` and shows output → `/code-review` and `/security-review` locally → PR with Testing, Risk, and How to revert filled in → AI review on GitHub → you approve personally only if it touches auth, billing, or prompt files.

- Next move: add `CLAUDE.md` with runnable checks and a `REVIEW.md` to your main repo, then run `/code-review` before each PR for a week and move repeated comments into `REVIEW.md`.
- Try it? Yes for pre-PR verification and `REVIEW.md`, since they take minutes. The risk-tier classifier and zero-human merges are only worth it if agents are opening many PRs a week.

- Add Testing, Risk, and How to revert sections to your PR template.
- Use CODEOWNERS and branch protection so auth, billing, and CI files always need a person.
- Never let a bot approval count as a human one, and dismiss approvals on new commits.
- Pick Quick, Standard, or Deep review depth based on what a missed bug costs.
- To learn a module, ask Claude for an explainer of that slice instead of reading trivial diffs.

[How the Claude Code team does code review](https://claude.dev/blog/solving-code-review-at-anthropic/)

**1. [How the Claude Code team does code review](https://claude.dev/blog/solving-code-review-at-anthropic/)**
- **What is it:** An audit process in several layers for the code that agents write:
  - The code is verified even before PR is opened.
  - Several agents search for bugs, and a separate group points out each finding before it is published.
  - security review can block merging.
  - classifier marks the risk level of each change, according to which it is determined how many people need to approve.
  - Underneath all this there is a merge queue, feature flags and fast rollback.
- **Why new:** AI review itself is not new. The new mechanisms are:
  - Every incident and revert from the past enters the eval that the tester runs against every day.
  - Noise is measured by how the author responded to each comment.
  - There is a ceiling of 3 rounds, followed by a re-review only on the new diff. The cap was put in place after one night where a writing agent and a checking agent went through more than 50 rounds.
  - The `REVIEW.md` file that the code owners write, with instructions for the tester.
- **Evidence:** These are data that the team reports, and no one from the outside has reproduced them:
  - Between June and September the number of merged PRs more than doubled, and the rate of reverts decreased by more than 40%.
  - The percentage of PRs that receive substantial comments increased from 16% to 54%.
  - There is also an independent signal: PostgreSQL 19 delayed to November after LLM review found more small bugs than humans can fix ([The Register](https://www.theregister.com/databases/2026/10/16/postgres-19-delayed-after-ai-reviewers-find-more-bugs-than-humans-can-fix/5303471)).
- **Scores:** Effectiveness 4/5, Hype 2/5.
- **Fit:** High for any product where agents make changes or actions, not just write code. Three patterns you can take:- The level of risk is determined according to the change, not according to who wrote it.
  - Convert incidents to eval.
  - Put a cap on rounds in the loop between the agent who executes and the agent who checks.
- **Effort:** Medium.
- **Recommendation: Adopt** for patterns. This is a direct follow up to yesterday's Scion.

## 4. Copy the Claude Code team's review recipe: Enterprise feasibility High | Stage Trial
- **What changed:** [Anthropic's post](https://claude.dev/blog/solving-code-review-at-anthropic/) (457 points on [HN](https://news.ycombinator.com/item?id=50122951), also quoted by [Simon Willison](https://simonwillison.net/2026/Oct/16/code-review/)) says merged PRs more than doubled from June to September while the share of reverts fell by more than 40%. Their recipe is AI review on every PR, risk tiers set by what the change touches, a cap of 3 review rounds, and a nit cap. Code Review is now generally available on Team and Enterprise.
- **How ​​it works:** commit a `REVIEW.md`. Code Review reads it from the base branch, so a PR can't rewrite its own review rules. In admin settings, set review runs to once after PR creation, since the default re-runs on every push and multiplies cost, and set a monthly spend limit.
- **Effort:** ~30 min.
- **PoC:**
```markdown
# REVIEW.md

## Always check
- **Sources:** [customize docs](https://code.claude.com/docs/en/code-review-customize), [costs docs](https://code.claude.com/docs/en/code-review-costs) (seen in 4 sources)

```

## Sources

- [How the Claude Code team does code review](https://claude.dev/blog/solving-code-review-at-anthropic/)
- [HN](https://news.ycombinator.com/item?id=50122951)
- [Simon Willison](https://simonwillison.net/2026/Oct/16/code-review/)
- [customize docs](https://code.claude.com/docs/en/code-review-customize)
- [Official): code-review plugin](https://github.com/anthropics/claude-plugins-official/tree/main/plugins/code-review)
- [The Register](https://www.theregister.com/databases/2026/10/16/postgres-19-delayed-after-ai-reviewers-find-more-bugs-than-humans-can-fix/5303471)
- [costs docs](https://code.claude.com/docs/en/code-review-costs)