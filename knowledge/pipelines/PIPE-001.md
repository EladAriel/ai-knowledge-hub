# PIPE-001: Reliable scheduled agent automations (bookmarks + ledger)

## Summary

Scheduled briefs lie with fixed 24h windows and silent source failures; use per-source bookmarks, a ledger and re-checks.

## Details

Setup: sources, one destination, agent.md run steps, cron, memory for preferences/state, guardrails on spend and read-only access. Flow: read from per-source bookmarks -> decide what earns a line -> re-check live status -> post only if Slack returns ok -> update ledger and bookmarks; on source failure keep its bookmark, brief the rest, name the gap. Never treat a failed read as a quiet day; cap spend per run. Next move: /claude-api managed-agents-onboard \<article URL>.

## Content

**Building effective agent automations** (Lance Martin and CJ Avilla)

- Scheduled agents that gather Slack and GitHub context and ping you beat manual triage. But fixed "last 24h" windows and silent source failures make them lie, like reporting "nothing new" when a connector is down.
- The trade-off is that reliable briefs need bookmarks, a ledger, and re-checks, which means more state and stricter run steps than a one-shot prompt.

- If you ship React, Python, or TypeScript AI apps with standing digests (open PRs, review blockers, support threads), a quiet miss costs more trust than a short empty day.

- The setup is sources, one destination, `agent.md` run steps, cron deployment, memory for preferences and state, and guardrails on spend and read-only access.
- Flow: read from per-source bookmarks → decide what earns a line → re-check live status → post only if Slack returns `ok` → update ledger and bookmarks. If a source fails → keep its bookmark → brief the rest → name the gap in one line.

Example

- In a TypeScript fullstack app, a Managed Agent reads your repo's open PRs through GitHub MCP and `#eng` in Slack, then posts "Daily brief, Fri Oct 9" with only actionable review blockers. Preferences live in a read-only store (channels, repos, length cap), and state holds `bookmarks.json` and `ledger.md`, so a late run stretches the window instead of skipping and yesterday's "still waiting, day 2" isn't reported as new.

- Next move: run `claude update`, then `/claude-api managed-agents-onboard https://claude.dev/blog/building-effective-agent-automations/` and customize the sources for your app.
- Should you try it? Yes if you want a standing PR and Slack brief and have Claude Managed Agents (beta) plus Slack and GitHub tokens. Only trust it unsupervised if you seed preferences and a spend cap first.

- Bookmark each source instead of using a fixed time window.
- Treat a failed read as unreadable, never as a quiet day.
- Confirm the Slack post before moving bookmarks or the ledger.
- Cap spend per run, and keep GitHub and preferences read-only.

[Building effective agent automations](https://claude.dev/blog/building-effective-agent-automations/)

## Sources

- [Building effective agent automations](https://claude.dev/blog/building-effective-agent-automations/)