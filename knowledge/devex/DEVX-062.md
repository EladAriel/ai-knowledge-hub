# DEVX-062: permissions.denyInsteadOfPrompting for unattended terminal, subagent and teammate sessions (Claude Code 2.1.319)

## Summary

New in 2.1.319: with permissions.denyInsteadOfPrompting, a tool call that would wait on a permission prompt is denied and the turn continues, so unattended runs fail closed instead of hanging.

## Details

Add the key under permissions in user or managed settings on 2.1.319+; pair with explicit permissions.allow for tools CI should use. The settings-reference index may still lag the changelog; confirm in /permissions after setting it.
PoC: { "permissions": { "denyInsteadOfPrompting": true } }
Success metric: an unattended session that would have waited on a prompt denies the call, continues the turn and does not hang; allowed tools still run.
Feasibility High, stage Trial; seen in 2 sources.

## Content

### 4. For unattended terminal, subagent and teammate sessions, set `permissions.denyInsteadOfPrompting` — Enterprise feasibility: High | Stage: Trial
- **What changed:** new in 2.1.319. A tool call that would wait on a permission prompt is denied and the turn continues, in terminal sessions, subagents and teammates.
- **How it works:** add the key under `permissions` in user or managed settings on 2.1.319+. Unattended runs fail closed instead of hanging. Pair with explicit `permissions.allow` for tools CI should use. The settings-reference index may still lag the changelog; confirm in `/permissions` after setting it.
- **Effort:** ~10 min
- **PoC:**
```json
{
  "permissions": {
    "denyInsteadOfPrompting": true
  }
}
```
- **Success metric:** an unattended session that would have waited on a permission prompt instead denies the call, continues the turn, and does not hang; allowed tools still run.
- **Sources:** [v2.1.319](https://github.com/anthropics/claude-code/releases/tag/v2.1.319), [changelog](https://code.claude.com/docs/en/changelog) | seen in 2 sources

## Sources

- [v2.1.319](https://github.com/anthropics/claude-code/releases/tag/v2.1.319)
- [changelog](https://code.claude.com/docs/en/changelog)
