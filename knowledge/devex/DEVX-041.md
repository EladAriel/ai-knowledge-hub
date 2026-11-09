# DEVX-041: Alert: Claude Code 2.1.317 changes headless/CI behavior; npm stable 2.1.309 -> 2.1.311

## Summary

Four behavior changes scripts may depend on: nested claude -p gets its own session ID, claude -p exits 1 on lost transcript writes, unchanged-file re-reads return full content, subagents on another model use that model's effort.

## Content

**[Claude Code 2.1.317 (latest) changes headless and CI behaviour, and npm `stable` moved from 2.1.309 to 2.1.311](https://github.com/anthropics/claude-code/releases/tag/v2.1.317)**
- **summary:** 2.1.317 was published to npm on Nov 2 at 23:57Z (Nov 3 01:57 Israel time); the GitHub release followed at 01:25Z (03:25 Israel time). It changes four things that scripts may depend on. (1) `claude -p` started inside a cloud or self-hosted-runner session now gets its own session ID and transcript. Before, it wrote into the parent session, and a restart could resume the wrong conversation. Set `CLAUDE_CODE_DISABLE_NESTED_SESSION_ID=1` to get the old behaviour back. (2) `claude -p` now exits 1, with an error, when a full disk or quota loses its transcript or `~/.claude.json` writes. It used to exit 0, so CI jobs on runners that are nearly full can start failing. Full NFS exports may still be missed. (3) The Read tool's 'file unchanged since your last Read' stub is gone, so reading an unchanged file again returns its full content, which can cost more tokens. (4) Subagents and teammates on a different model from the main conversation now use that model's saved or default effort, not the session's effort. Separately, npm dist-tag `stable` moved from 2.1.309 to 2.1.311 (latest=next=2.1.317), so fleets pinned to the stable channel jump two versions.
- **verified:** true

## Sources

- [Claude Code v2.1.317 release](https://github.com/anthropics/claude-code/releases/tag/v2.1.317)
