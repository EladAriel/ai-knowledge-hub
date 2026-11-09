# DEVX-005: Cursor guardrails rule

## Summary

Base rules that are always loaded for each agent in the repo.

## Content

**[Cursor guardrails rule — adapted from Cursor docs](https://cursor.com/docs/context/rules)**
Base rules that are always loaded for each agent in the repo. **Effort:** ~5 minutes. File `.cursor/rules/guardrails.mdc`:
```markdown
---
alwaysApply: true
---
- When unsure about implementation details, read the relevant source files before proposing changes
- Never modify generated files in `dist/` or `build/`
- Never commit secrets or credentials; use env vars
```

---
*Resources that were not available: arXiv API (timeout), Anthropic news (did not load), r/ClaudeAI (not completed). No new entries this week: Cursor changelog, Aider (last version v0.86.0, Aug 2025), The Changelog (not relevant episode).*

## Sources

- [Cursor rules docs](https://cursor.com/docs/context/rules)