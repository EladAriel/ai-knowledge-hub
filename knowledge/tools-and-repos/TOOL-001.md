# TOOL-001: security-auditor subagent (wshobson/agents)

## Summary

Dedicated security checker for OWASP, auth and secrets that can be run on any feature (40.3k★, MIT).

## Content

**[security-auditor subagent — wshobson/agents](https://github.com/wshobson/agents/blob/main/plugins/backend-development/agents/security-auditor.md)** (40.3k★, MIT, latest push 5.10)
Dedicated security scanner for OWASP, auth and secrets that can be run on any feature. **Effort:** ~5 minutes
```bash
/plugin marketplace add wshobson/agents
/plugin install backend-development@claude-code-workflows
```
Or a minimal file, adapted from the source, in `.claude/agents/security-auditor.md`:
```markdown
---
name: security-auditor
description: Review code for OWASP Top 10, auth flaws, secrets. Use for security review during feature development.
model: sonnet
---
You are a security auditor. Scan the changed code for injection, broken access control,
secrets in source, SSRF and vulnerable dependencies. Report severity + fix per finding.
```

## Sources

- [security-auditor subagent](https://github.com/wshobson/agents/blob/main/plugins/backend-development/agents/security-auditor.md)