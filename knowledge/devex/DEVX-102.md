# DEVX-102: A practical guide to shipping with Claude Code

## Summary

After you open a pull request, failed checks, review comments, and merge conflicts keep pulling you off the work you meant to do next. Claude Ship hands that follow-up to Claude Code. `/code-review` checks your branch before you push, `/ship` can commit, open the PR, and review it, and `/steward` looks after a PR you already opened. Code Review is generally available; PR Steward and Claude Approvals are still in beta. Ultra review runs in the cloud, may be billed separately, and needs a claude.ai login. `--fix` during a background review may not be caught by `/rewind`, so commit first if you want an easy way back. You stay in charge of what to build and when to merge, and you can start on your own PRs with no admin access.

## Details

- Why it matters: if you ship React, Python, or TypeScript apps and lose flow every time a small review comment or a failed check shows up.
- How it works: branch changes → `/code-review` or `/ship` → findings or fixes land on the PR → you decide whether to merge.
- Next step: only if you already use Claude Code with GitHub, run `/code-review` a few times first so you learn what it catches and where it is wrong, then try `/ship` on your next PR.
- Verdict: yes to `/code-review` now; only-if for `/ship` after that; skip rolling it out across the team until you trust the results.
- Availability: Code Review is GA; PR Steward and Claude Approvals are in beta. Ultra review runs in the cloud, may be billed separately, and needs a claude.ai login.
- Caveat: `--fix` during a background review may not be caught by `/rewind`, so commit first if you want an easy way back.
- Published Nov 25. The same product is covered as a pattern in METH-209 (Pilot). Related: DEVX-019 (`/code-review` as a pre-PR CI step).

## Content

### Examples

- Example. Run `/code-review --fix` on a Python API change before you push, so obvious bugs never become review threads.
- Example. Use `/code-review high` on a risky React form refactor when you want more findings, including ones it is less sure about.

## Sources

- [A practical guide to shipping with Claude Code](https://claude.dev/blog/the-work-after-you-open-a-pr/)
