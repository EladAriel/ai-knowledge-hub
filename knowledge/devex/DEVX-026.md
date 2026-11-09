# DEVX-026: Manual-only side-effect skills

## Summary

Claude can't start '/deploy' or '/commit' on its own, so a person has to type the command.

## Details

Source: Claude Code docs. Skill frontmatter 'disable-model-invocation: true', or settings skillOverrides { 'deploy': 'off' }.

## Sources

- [skills docs](https://code.claude.com/docs/en/skills)
