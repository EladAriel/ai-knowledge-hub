# DEVX-022: Allow only org-approved Claude Code mods (one managed key)

## Summary

Mods (plugins that run code inside Claude Code) are on by default and now ship on stable.

## Details

With neither managed settings nor a Team/Enterprise login, a mod can approve a call your deny rule or PreToolUse hook blocked. That covers API-key, Bedrock, Vertex and CI token setups. ….

## Sources

- [mods admin docs](https://code.claude.com/docs/en/plugins/mods/admin)
- [v2.1.304 notes](https://github.com/anthropics/claude-code/releases/tag/v2.1.304)
