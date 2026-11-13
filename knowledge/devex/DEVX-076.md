# DEVX-076: /fewer-permission-prompts: a bundled Claude Code skill that builds an allowlist from your own transcripts

## Summary

A skill bundled with Claude Code scans past sessions for read-only Bash and MCP calls you kept approving and writes a prioritized allowlist into the project's .claude/settings.json. Fewer prompts means less rubber-stamping; the list is a reviewable file you can commit for the team. Feasibility High, stage Adopt, ~5 min.

## Details

PoC: run `/fewer-permission-prompts` in a repo, then `git diff .claude/settings.json`. Before committing, delete anything that writes, deletes or touches the network.
Success metric: permission prompts per session, before and after. Seen in 2 sources. Expires Feb 9, 2027.

## Content

### 3. `/fewer-permission-prompts`: an allowlist built from your own transcripts — Enterprise feasibility: High | Stage: Adopt
- What changed: a skill bundled with Claude Code scans your past sessions for read-only Bash and MCP calls you kept approving. It writes a prioritized allowlist into the project's `.claude/settings.json`.
- Why it matters: fewer prompts means less rubber-stamping, so the prompts that are left get real attention. The list is a reviewable file, so you can commit it for the whole team.
- Effort: ~5 min.
- PoC: run `/fewer-permission-prompts` in a repo, then `git diff .claude/settings.json`. Before you commit, delete anything that writes, deletes or touches the network.
- Success metric: permission prompts per session, before and after.
- Sources: [commands reference](https://code.claude.com/docs/en/commands), [X tip](https://x.com/TheAIToolbelt/status/2120189193670594680) | seen in 2 sources | expires Feb 9, 2027

## Sources

- [commands reference](https://code.claude.com/docs/en/commands)
- [X tip](https://x.com/TheAIToolbelt/status/2120189193670594680)
