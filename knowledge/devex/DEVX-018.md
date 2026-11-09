# DEVX-018: Cursor Bugbot config + BUGBOT.md

## Summary

The Cursor version of the Claude Code review recipe. It reviews once per PR, skips drafts, and keeps autofix off. Rules are read from the base branch, and '.cursor/rules' doesn't apply to Bugbot.

## Details

It reviews once per PR, skips drafts, and keeps autofix off. Rules are read from the base branch, and '.cursor/rules' doesn't apply to Bugbot. Credit: Cursor docs. ….

## Sources

- [Cursor Bugbot docs](https://cursor.com/docs/bugbot)
