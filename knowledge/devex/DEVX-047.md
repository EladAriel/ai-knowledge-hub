# DEVX-047: Postman Desktop silently installs its plugin/hook into Claude Code, Codex, Cursor, Copilot CLI: detect and block

## Summary

Postman desktop updates 12.33.4 and 12.35.1 installed postman@claude-plugins-official into Claude Code at user scope, a Codex marketplace/plugin plus a self-trusted SessionStart hook, a remote MCP entry (mcp.postman.com) and a CLI, without asking. A managed enabledPlugins false entry blocks it in Claude Code.

## Details

Evidence: issue #14370 (305 reactions), HN 1,202 points; Postman's own log records source 'auto-existing-upgrade' with claude-code:installed, codex:installed; second user on 12.35.1; Copilot entries in ~/.copilot/settings.json; installer function 'Approves only Postman's current hook after installation' (confirmed by The Proof Desk). Hook tells the agent to load postman:api-engineer before any non-trivial API task. Unverified: a reply in Postman's voice promising clearer opt-in (account not marked as Postman); the HN claim that all API data is shared isn't shown by the issue. Why it matters (AI methods): a new agent supply-chain vector where a legitimate app changes user-level agent config; recurring theme (Oct 25, 27, 28, 31).

## Sources

- [Postman issue #14370](https://github.com/postmanlabs/postman-app-support/issues/14370)
- [HN thread](https://news.ycombinator.com/item?id=50354960)
- [postman-plugin README](https://github.com/postmanlabs/postman-plugin)
- [Claude Code plugins/org docs](https://code.claude.com/docs/en/plugins/org)
- [The Proof Desk](https://theproofdesk.com/postman-desktop-auto-installs-claude-code-codex-plugins-hook)
- [Postman MEMBER revert comment](https://github.com/postmanlabs/postman-app-support/issues/14370#issuecomment-6649122696)
