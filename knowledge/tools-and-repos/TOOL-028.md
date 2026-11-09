# TOOL-028: Official mcp-builder skill, updated

## Summary

(Anthropic, Oct 28) new internal MCP servers start on TypeScript SDK v2 and come with a self-check script.

## Content

**[Official mcp-builder skill, updated](https://github.com/anthropics/skills/tree/main/skills/mcp-builder)** (Anthropic, Oct 28): new internal MCP servers start on TypeScript SDK v2 and come with a self-check script. Effort ~5 min.
```
/plugin marketplace add anthropics/skills
/plugin install example-skills@anthropic-agent-skills
```

Footnote: `forceLoginMethod: "console"` alone doesn't block keyless Console sign-in. Use `"claudeai"` or an MDM-deployed `forceLoginOrgUUID`. Note that `forceLoginOrgUUID` refuses API-key and `apiKeyHelper` sessions, which can break gateway setups.

## Sources

- [mcp-builder](https://github.com/anthropics/skills/tree/main/skills/mcp-builder)
