# DEVX-026: Manual-only side-effect skills

## Summary

Claude can't start '/deploy' or '/commit' on its own, so a person has to type the command.

## Details

Source: Claude Code docs. Skill frontmatter 'disable-model-invocation: true', or settings skillOverrides { 'deploy': 'off' }.

## Content

**[Manual-only side-effect skills](https://code.claude.com/docs/en/skills):** Claude can't start `/deploy` or `/commit` on its own, so a person has to type the command. ~10 min. Source: Claude Code docs.
```yaml
---
name: deploy
description: Deploy the application to production
disable-model-invocation: true
---
```
```json
{ "skillOverrides": { "deploy": "off" } }
```

## Sources

- [skills docs](https://code.claude.com/docs/en/skills)