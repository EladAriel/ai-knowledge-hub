# DEVX-048: Alert: Claude Code 2.1.318 is latest (stable still 2.1.311): runner logs, deniedMcpServers, IDE extension, ~/.claude.json behavior change

## Summary

Breaking-change alerts - Claude Code 2.1.318 is now latest; npm stable is still 2.1.311. Released Nov 4 at 01:55 Israel time (release notes). Self-hosted runner log lines changed: ok session=... now prints at every log level, and nack lines now end with reason=..., so update any scripts that match retryable=true: or retryable=false:.

## Details

Also: /claude-api managed-agents-onboard gives new agents' built-in tools the 'auto' permission policy by default; background subagents move a shell command to the background after 3 minutes on all providers; the 2.1.288 fix keeping earlier thinking when resuming conversations started on 2.1.286 or earlier was removed. npm published Nov 3 21:55Z (23:55 Israel), GitHub release Nov 4 00:00Z; latest=next=2.1.318.

## Content

## Breaking-change alerts
- **Claude Code 2.1.318 is now latest; npm `stable` is still 2.1.311.** Released Nov 4 at 01:55 Israel time ([release notes](https://github.com/anthropics/claude-code/releases/tag/v2.1.318)). Self-hosted runner log lines changed: `ok session=…` now prints at every log level, and `nack` lines now end with `reason=…`, so update any scripts that match `retryable=true:` or `retryable=false:`. URL entries in `deniedMcpServers` now also block matching servers that Anthropic provides, and connectors in cloud sessions. Claude Code no longer installs its IDE extension on its own. A broken `~/.claude.json` now fails non-interactive runs instead of being silently reset. Resuming old conversations no longer keeps earlier thinking.

## Sources

- [Claude Code v2.1.318 release](https://github.com/anthropics/claude-code/releases/tag/v2.1.318)