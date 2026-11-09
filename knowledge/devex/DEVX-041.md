# DEVX-041: Alert: Claude Code 2.1.317 changes headless/CI behavior; npm stable 2.1.309 -> 2.1.311

## Summary

Four behavior changes scripts may depend on: nested claude -p gets its own session ID, claude -p exits 1 on lost transcript writes, unchanged-file re-reads return full content, subagents on another model use that model's effort.

## Details

(1) claude -p started inside a cloud or self-hosted-runner session now gets its own session ID and transcript (before, it wrote into the parent session and a restart could resume the wrong conversation); set CLAUDE_CODE_DISABLE_NESTED_SESSION_ID=1 for the old behavior. (3) The Read tool's 'file unchanged' stub is gone: re-reading an unchanged file returns full content (more tokens). (4) Subagents/teammates on a different model use that model's saved or default effort, not the session's. npm dist-tag stable moved 2.1.309 -> 2.1.311 (latest=next=2.1.317), so fleets pinned to stable jump two versions.

## Sources

- [Claude Code v2.1.317 release](https://github.com/anthropics/claude-code/releases/tag/v2.1.317)
