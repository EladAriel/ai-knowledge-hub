# DEVX-002: Claude Code cloud sessions

## Summary

Each task gets a fresh VM with the repo cloned on a new branch; parallel tasks don't collide and keep running while the laptop sleeps.

## Details

claude --cloud "task" (or claude.ai/code, mobile, Desktop, Slack); clones the pushed branch, runs setup, works on its own branch; GitHub token stays in a proxy; repo CLAUDE.md, .claude hooks/skills and .mcp.json come along, personal config doesn't. Finish with a PR or claude --teleport. Example: SessionStart hook runs pnpm install/uv sync, UserPromptSubmit hook appends conventions; 'fix flaky test, prove with 30 runs'. Uses: one session per small backlog fix, loop flaky tests 40x, plan locally/build in cloud, Auto-fix for CI failures, sessions from routines/HTTP/GitHub events, untrusted PRs with network None. Verdict: yes for small parallel fixes.

## Content

**Claude Code in the cloud: a field guide to cloud sessions** (Oct 6, Addy Osmani)

- Cloud sessions give each Claude Code task its own fresh virtual machine, with your repo cloned onto a new branch. Parallel tasks never fight over files or ports, and they keep running when your laptop sleeps.
- The trade-off is isolation. Sessions can't see each other's fixes or reach your local database, VPN, or `~/.claude`, and idle machines get reclaimed, so commit as you go.

- For React, Python, and TypeScript apps, you can start several small backlog fixes at once and come back to branches ready for review, without juggling worktrees.
- It's also a safe sandbox for untrusted PRs or new dependencies, kept away from your SSH keys and cloud credentials.

- You start a session with `claude --cloud "task"` or from claude.ai/code, mobile, Desktop, or Slack. It clones your pushed branch, runs your setup, and works on its own branch.
- Your GitHub token stays in a proxy outside the machine. The repo's `CLAUDE.md`, `.claude/` hooks and skills, and `.mcp.json` come along, but your personal config doesn't.
- When it's done, you open a PR, or pull the session into your terminal with `claude --teleport`.

Example

- In a Next.js plus FastAPI app, commit a `UserPromptSubmit` hook in `.claude/settings.json` that appends `docs/conventions.md` (Zod schemas, pytest fixtures, no default exports) to every prompt. Add a `SessionStart` hook that runs `pnpm install` and `uv sync`.
- Flow: push branch → `claude --cloud "Fix the flaky useCart test, prove it with 30 runs of pnpm vitest"` → SessionStart installs deps → prompt hook adds your conventions → Claude fixes and loops the tests → branch → review diff → Create PR.

- Next move: connect GitHub at claude.ai/connect-github and install the Claude GitHub App on the account that owns your repo. Then hand it one backlog task along with a command that proves it's done.
- If you're on Pro or Max, today, October 7, is the last day to claim the one-time cloud credit ($100 on Pro, $250 on Max) at claude.ai/code/claim-credit.

- Yes, try it for small parallel fixes, flaky tests, and keeping docs in sync with code. Stay local only if the task needs local data, a VPN service, or a tight visual loop.

- Clear a backlog by starting one cloud session per small fix and reviewing each branch.
- Prove a flaky-test fix by looping the suite 40 times or more on the cloud machine's CPU instead of yours.
- Plan locally in plan mode, build in the cloud, then use `claude --teleport` to finish by hand.
- Turn on Auto-fix so Claude pushes fixes for failing CI checks and review comments on a PR.
- Start sessions from a routine on a schedule, an HTTP call, or a GitHub event.
- Run an untrusted contributor PR in a throwaway machine with network access set to None.

[Claude Code in the cloud: a field guide to cloud sessions](https://claude.dev/blog/claude-code-in-the-cloud/)

## Sources

- [Claude Code in the cloud](https://claude.dev/blog/claude-code-in-the-cloud/)