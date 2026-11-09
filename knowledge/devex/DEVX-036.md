# DEVX-036: Weekend Scope Guard (Cursor rules)

## Summary

Two always-on Cursor rules: at most 5 files changed and 3 created per request, no new dependency without asking, don't call work done without test steps.

## Details

mkdir -p .cursor/rules && cp weekend-scope-guard/rules/*.mdc .cursor/rules/ . MIT, brand new project but plain text.

## Content

- **[Weekend Scope Guard](https://github.com/weekendshipkit/weekend-scope-guard)** (Cursor rules, MIT) is two always-on rules: change at most 5 files and create at most 3 per request, add no new dependency without asking, and don't call work done without test steps. The project is brand new, but it's plain text. Effort is about 5 min.
```bash
mkdir -p .cursor/rules && cp weekend-scope-guard/rules/*.mdc .cursor/rules/
```

## Sources

- [weekend-scope-guard](https://github.com/weekendshipkit/weekend-scope-guard)