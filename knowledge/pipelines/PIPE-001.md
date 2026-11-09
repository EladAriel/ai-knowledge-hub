# PIPE-001: Reliable scheduled agent automations (bookmarks + ledger)

## Summary

Scheduled briefs lie with fixed 24h windows and silent source failures; use per-source bookmarks, a ledger and ….

## Details

Setup: sources, one destination, agent.md run steps, cron, memory for preferences/state, guardrails on spend and read-only access. Flow: read from per-source bookmarks -> decide what earns a line -> re-check live status -> post ….

## Sources

- [Building effective agent …](https://claude.dev/blog/building-effective-agent-automations/)
