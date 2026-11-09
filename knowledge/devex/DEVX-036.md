# DEVX-036: Weekend Scope Guard (Cursor rules)

## Summary

Two always-on Cursor rules: at most 5 files changed and 3 created per request, no new dependency without asking, don't call work done without test steps.

## Details

mkdir -p .cursor/rules && cp weekend-scope-guard/rules/*.mdc .cursor/rules/ . MIT, brand new project but plain text.

## Sources

- [weekend-scope-guard](https://github.com/weekendshipkit/weekend-scope-guard)
