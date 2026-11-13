# DEVX-064: whoami-guard: PreToolUse hook that blocks your own email/name going out (Claude Code and Codex)

## Summary

A local PreToolUse hook for Claude Code and Codex that denies calls sending your own email or name via User-Agent / curl -A, WebFetch, MCP, or Write/Edit, covering surfaces the built-in privacy mod doesn't. Surfaced on #107757 on Nov 6; MIT, small project, Trial only.

## Details

Repo created Oct 30; PyPI 0.2.2 on Nov 1. Install: uv tool install whoami-guard. Hook config: PreToolUse matcher "Bash|PowerShell|WebFetch|Write|Edit|MultiEdit|mcp__.*" running command whoami-guard-hook with onFailure block and timeout 10. Identity file at ~/.egress-guard/identity.json with emails, names, extra, allow_hosts, ignore, strict, autodetect (full JSON below). Related: the earlier DevEx item 'PreToolUse hook: block your email from going out in tool calls' (Nov 1) and DEVX-061 on the built-in privacy mod (Nov 8).

## Content

**[whoami-guard](https://github.com/ChrystianSchutz/whoami-guard)** is a local PreToolUse hook for Claude Code and Codex that denies calls sending your own email or name via User-Agent/`curl -A`, WebFetch, MCP, or Write/Edit. Surfaced on [#107757](https://github.com/anthropics/claude-code/issues/107757) on Nov 6 (repo created Oct 30; PyPI 0.2.2 on Nov 1). MIT, small project — Trial only. Effort: ~15 min.
```bash
uv tool install whoami-guard
```
```json
{
  "hooks": {
    "PreToolUse": [
      {
        "matcher": "Bash|PowerShell|WebFetch|Write|Edit|MultiEdit|mcp__.*",
        "hooks": [
          {
            "type": "command",
            "command": "whoami-guard-hook",
            "onFailure": "block",
            "timeout": 10
          }
        ]
      }
    ]
  }
}
```
```json
{
  "emails": ["you@your-mail.com"],
  "names": ["First Last"],
  "extra": ["+48 600 000 000"],
  "allow_hosts": ["github.com"],
  "ignore": ["firstlast-blog"],
  "strict": false,
  "autodetect": true
}
```
Put the identity file at `~/.egress-guard/identity.json`.

## Sources

- [whoami-guard](https://github.com/ChrystianSchutz/whoami-guard)
- [#107757](https://github.com/anthropics/claude-code/issues/107757)
