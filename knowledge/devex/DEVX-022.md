# DEVX-022: Allow only org-approved Claude Code mods (one managed key)

## Summary

Mods (plugins that run code inside Claude Code) are on by default and now ship on stable.

## Content

### 2. Allow only org-approved Claude Code mods (one managed key) — Enterprise feasibility: High | Stage: Adopt
- **What changed:** mods (plugins that run code inside Claude Code) are on by default and now ship on stable. The permissions docs say that with neither managed settings nor a Team/Enterprise login, a mod can approve a call your deny rule or PreToolUse hook blocked. That covers API-key, Bedrock, Vertex and CI token setups. Mods also aren't sandboxed.
- **How it works:** any managed settings file loads the built-in guard, which keeps deny rules above mod approvals. `allowManagedModsOnly` then refuses every mod a user brings, while settings hooks and status lines keep working.
- **Effort:** ~15 min
- **PoC (verbatim from the docs):**
```json
{ "pluginConfigs": { "cc-plugin-sec-default@builtin": { "options": { "allowManagedModsOnly": true } } } }
```
```bash
claude --debug --plugin-dir ./any-mod   # expect: refused by cc-plugin-sec-default (allowManagedModsOnly)
```
- **Org challenge:** org mods need an admin-installed marketplace folder. The optional `"disableSideloadFlags": true` also blocks `--agents` and `--mcp-config`, so check your CI scripts before turning it on.
- **Success metric:** a test `--plugin-dir` mod is refused on every machine and CI image.
- **Sources:** [mods admin docs](https://code.claude.com/docs/en/plugins/mods/admin), [v2.1.304 notes](https://github.com/anthropics/claude-code/releases/tag/v2.1.304) | seen in 7 sources | expires: 2027-01-18

## Sources

- [mods admin docs](https://code.claude.com/docs/en/plugins/mods/admin)
- [v2.1.304 notes](https://github.com/anthropics/claude-code/releases/tag/v2.1.304)
