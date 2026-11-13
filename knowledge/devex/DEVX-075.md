# DEVX-075: Modern Web Guidance: browser-vendor skill + CLI that keeps agents off 2019-era JavaScript (with a browser-baseline Cursor rule)

## Summary

Chrome, Edge, Firefox and MDN teams released curated, eval-pruned guides (container queries, View Transitions, popover/dialog, accessibility, more) that the agent pulls in as needed instead of polyfills and old libraries. Skill plus CLI (search, retrieve, legacy-scan). Feasibility Medium, stage Trial, ~10 min.

## Details

Caveat (HN): it can suggest features with limited browser support, so put your browser baseline in AGENTS.md/CLAUDE.md.
PoC (pinned, no install): `npx modern-web-guidance@1.0.0 legacy-scan .` and `npx modern-web-guidance@1.0.0 search "animate a dialog modal backdrop"`; if useful, `npx skills add GoogleChrome/modern-web-guidance`.
Success metric: legacy-scan findings on the React frontend, and fewer new deps (polyfills, animation libraries) in agent PRs.
Health: Apache-2.0, ~3.5k stars, run by browser vendors; v1.0.0 came out Nov 10, so pin it. Show HN 344 points.
Mod: Cursor rule `.cursor/rules/web-baseline.mdc` (globs **/*.tsx, **/*.ts, **/*.css; alwaysApply false): target Baseline 'widely available' only, prefer native platform APIs over new deps/polyfills, never add a dependency for something the platform already does (an adaptation of the HN advice). Seen in 3 sources. Expires Feb 9, 2027. AI methods review, Nov 11 (effectiveness 4/5 · hype 2/5; recommendation Adopt): the novel bit is pruning the skill by evals so it keeps only what the model does not already know, which saves tokens; platform vendors maintain the knowledge. Runnable code and a public evals dashboard. Project-own evals (not independent) on 215 tasks: Claude Code 57% to 88%, Codex 54% to 82%. 3.5k stars and 350 points on HN. Immediate fit for any product that generates web code; the pattern of a skill that keeps only what the model does not know, pruned by evals, also fits any organisational knowledge pack. Effort low.

## Content

### 2. Modern Web Guidance: a skill that keeps agents off 2019-era JavaScript — Enterprise feasibility: Medium | Stage: Trial
- What changed: the Chrome, Edge, Firefox and MDN teams released curated, eval-pruned guides (container queries, View Transitions, popover and dialog, accessibility, and more) that the agent pulls in as needed instead of reaching for polyfills and old libraries. Show HN got 344 points.
- How it works: a skill plus a CLI with `search`, `retrieve` and `legacy-scan`. HN commenters warn that it can suggest features with limited browser support, so put your browser baseline in `AGENTS.md`/`CLAUDE.md`.
- Effort: ~10 min.
- PoC (try it without installing, pinned):
  ```bash
  npx modern-web-guidance@1.0.0 legacy-scan .
  npx modern-web-guidance@1.0.0 search "animate a dialog modal backdrop"
  ```
  If the scan is useful, install the skill with `npx skills add GoogleChrome/modern-web-guidance`.
- Success metric: findings from `legacy-scan` on your React frontend, and fewer new deps such as polyfills and animation libraries in agent PRs.
- Health: Apache-2.0, about 3.5k stars, pushed yesterday, run by browser vendors (low bus-factor risk). v1.0.0 came out Nov 10, so pin it.
- Sources: [repo](https://github.com/GoogleChrome/modern-web-guidance), [Show HN thread](https://news.ycombinator.com/item?id=50443812), [docs](https://developer.chrome.com/docs/modern-web-guidance) | seen in 3 sources | expires Feb 9, 2027

- [Cursor rule: browser baseline](https://news.ycombinator.com/item?id=50443812): pairs with item 2 so modern-API suggestions stay within the browsers you support. ~2 min. Save as `.cursor/rules/web-baseline.mdc`:
```markdown
---
description: Web platform baseline for frontend code
globs: ["**/*.tsx", "**/*.ts", "**/*.css"]
alwaysApply: false
---
- Target Baseline "widely available" features only; anything newer needs a feature check and a lightweight fallback.
- Prefer native platform APIs (dialog, popover, container queries) over new dependencies or polyfills.
- Never add a dependency for something the platform already does; say which API you used instead.
```

Credit: the baseline rule is an adaptation of the HN thread's advice.

## Sources

- [repo](https://github.com/GoogleChrome/modern-web-guidance)
- [Show HN thread](https://news.ycombinator.com/item?id=50443812)
- [docs](https://developer.chrome.com/docs/modern-web-guidance)
