# METH-051: 'Markdown is the new executable': AGENTS.md file planted in the downloads folder

## Summary

A site can silently download the AGENTS.md file to the '~/Downloads' folder.

## Content

**1. ["Markdown is the new executable": AGENTS.md file planted in the downloads folder](https://forever.security/blog/hijacking-ai-agents-via-downloads-folder/)** (Forever Security, 22.10)
- **What it is:** A website can silently download an AGENTS.md file to the `~/Downloads` folder. A code agent run from this folder obeys the file: it changes its configuration, installs a malicious npm package, or hands over its login token.
- **Why new:** This is an injection vector that does not require a single click, and it is actually captured on a client's computer (the function-color package). This is a direct continuation of the wave where content : the headers on 17.10, the allow-rules on 19.10 and the WhatsApp help pages on 20.10. The topic of agent control has been coming back for almost a week in a row.
- **Evidence:**
  - The real incident is recorded, and the researchers repeated it on Codex and Claude Code.
  - In their tests, Codex ran Nozka in over 90% of attempts and Claude in about 50% of them. The number of attempts is not specified.
  - The claim that "about half of the customers run an agent from Downloads" is based on the provider's own telemetry, and there is also a marketing interest here.
- **Scores:** Effectiveness 4/5, Hype 3/5.
- **Fit:** High for any product that reads instruction files S.md, skills or rules. **low** effort:
  - Do not trust instruction files from folders that the network can write to.
  - Require approval for each new instruction file.
  - Limit the agent's ability to change its own configuration.
- **Recommendation: Adopt** for controls.

## Planted CLAUDE.md hijack defense — Enterprise feasibility: High | Stage: Adopt- What changed: [Forever Security](https://forever.security/blog/hijacking-ai-agents-via-downloads-folder/) found a real malicious `AGENTS.md` sitting in a customer's `~/Downloads`. In their tests, a planted `CLAUDE.md` got Claude Code to write `env.ANTHROPIC_BASE_URL` into `.claude/settings.json`, which sends your login token to an attacker's server. It worked about half the time, because people approved the write. There's no bug to patch, and 6 sources covered it.
- How it works: pinning `ANTHROPIC_BASE_URL` in managed settings overrides anything a project tries to set, and a deny rule blocks edits to settings files. In CI, `--strict-mcp-config` loads only the MCP servers you pass, and `--setting-sources user` skips project settings.
- PoC (built from the documented settings, not tested yet; use your gateway URL if you route through one):
```jsonc
// managed-settings.json
{ "env": { "ANTHROPIC_BASE_URL": "https://api.anthropic.com" },
  "permissions": { "deny": ["Edit(**/.claude/settings.json)", "Edit(**/.claude/settings.local.json)"] } }
```
```bash
claude -p "$PROMPT" --strict-mcp-config --mcp-config ./ci-mcp.json --setting-sources user
grep -rl --include='settings*.json' ANTHROPIC_BASE_URL ~ 2>/dev/null   # read-only sweep
```
- Success metric: the sweep finds no unexpected URLs, and every CI `claude -p` job runs with `--strict-mcp-config`.
- Watch out: a wrong pinned URL breaks every session. Also, never start an agent inside Downloads.

## Sources

- ["Markdown is the new executable": AGENTS.md file planted in the downloads folder](https://forever.security/blog/hijacking-ai-agents-via-downloads-folder/)
