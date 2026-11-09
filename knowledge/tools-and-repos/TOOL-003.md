# TOOL-003: HOL Guard, a local 'AI antivirus'

## Summary

Checks risky shell, file, MCP, plugin and skill actions on your machine before they run.

## Content

### 2. HOL Guard, a local "AI antivirus". Enterprise feasibility: High | Stage: Trial
- **What changed:** HOL Guard checks risky shell, file, MCP, plugin, and skill actions on your machine before they run, asks for approval, and keeps a receipt of each decision. It's actively maintained: version 3.42.0, 854★, Apache-2.0, last pushed today.
- **How it works:** It installs hooks into Claude Code or Cursor. Start with a dry run before enforcing anything.
- **Effort:** ~15 min
- **PoC:**
```bash
pipx install hol-guard
hol-guard init
hol-guard install claude-code
hol-guard run
```

Enterprise feasibility: Medium | Stage: Assess
- **What changed:** [PR #5131](https://github.com/modelcontextprotocol/servers/pull/5131) was merged today. One server process can now handle clients on the older 2025 protocol and on the new `2026-07-28` protocol, which Claude Code has used by default since v2.1.292. This is only on the main branch so far and isn't part of the published 1.0.0.
- **Effort:** ~20 min, once a release ships.
- **PoC:** Stay on 1.0.0 in production for now. When a numbered release with this change ships, test one old-protocol client and one new-protocol client against the same server.

## Sources

- [PR #5131](https://github.com/modelcontextprotocol/servers/pull/5131)
