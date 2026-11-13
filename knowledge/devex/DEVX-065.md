# DEVX-065: Stroq: local CLI that audits 30 days of Claude Code/Codex/Cursor sessions for secrets and installs egress-deny hooks

## Summary

A local, no-telemetry CLI that reads the last 30 days of Claude Code, Codex and Cursor sessions, prints key names but never values, and can install hooks that deny curl | sh and outbound calls carrying a known secret. Show HN Nov 5; Apache-2.0, Node 22+.

## Details

Repo from Sep 4, last push Nov 7. Commands: npx @stroq/cli; npx @stroq/cli init; npx @stroq/cli sent; npx @stroq/cli replay --all; npx @stroq/cli console.

## Content

**[Stroq](https://github.com/AGGIB/Stroq)** is a local no-telemetry CLI that reads the last 30 days of Claude Code/Codex/Cursor sessions, prints key names never values, and can install hooks that deny `curl | sh` and outbound calls carrying a known secret. Show HN Nov 5; repo from Sep 4, last push Nov 7. Apache-2.0, Node 22+. Effort: ~15 min.
```bash
npx @stroq/cli
npx @stroq/cli init
npx @stroq/cli sent
npx @stroq/cli replay --all
npx @stroq/cli console
```

## Sources

- [Stroq](https://github.com/AGGIB/Stroq)
