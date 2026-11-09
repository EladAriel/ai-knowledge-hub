# DEVX-048: Alert: Claude Code 2.1.318 is latest (stable still 2.1.311): runner logs, deniedMcpServers, IDE extension, ~/.claude.json behavior change

## Summary

Self-hosted runner log lines changed (ok session=… at every level on stdout; nack lines end with reason=…, update scripts matching retryable=true:/false:); deniedMcpServers URL entries now also block matching Anthropic-provided servers and connectors in cloud sessions and runners; no more IDE extension auto-install; invalid ~/.claude.json makes non-interactive runs fail instead of resetting.

## Details

Also: /claude-api managed-agents-onboard gives new agents' built-in tools the 'auto' permission policy by default; background subagents move a shell command to the background after 3 minutes on all providers; the 2.1.288 fix keeping earlier thinking when resuming conversations started on 2.1.286 or earlier was removed. npm published Nov 3 21:55Z (23:55 Israel), GitHub release Nov 4 00:00Z; latest=next=2.1.318.

## Sources

- [Claude Code v2.1.318 release](https://github.com/anthropics/claude-code/releases/tag/v2.1.318)
