# DEVX-001: Claude Code mods (plugin JS/TS middleware)

## Summary

Small JS/TS files inside plugins that hook session events, rewrite or block actions, and draw terminal UI; ….

## Details

Each mod exports register(on); hooks get $ (mods API), event e and next: next(e) passes, next({...e,changed}) rewrites, return {deny} refuses. Keep data in $.state (survives hot reload). ….

## Sources

- [Getting started with Claude …](https://claude.dev/blog/getting-started-with-claude-code-mods/)
