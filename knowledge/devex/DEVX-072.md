# DEVX-072: Pin one sandboxed settings file to every Remote Control session (claude remote-control --settings)

## Summary

2.1.321 added claude remote-control --settings \<file>, so sessions started from your phone or claude.ai run under the same sandbox as your terminal instead of your user settings. If the file changes, no new session starts until the server restarts. Feasibility Medium, stage Trial, ~5 min.

## Details

PoC: save rc-settings.json as { "sandbox": { "enabled": true, "failIfUnavailable": true, "allowUnsandboxedCommands": false } }, then run `claude remote-control --settings ./rc-settings.json`.
Success metric: every remote session shows the sandbox on in /status. Seen in 1 source. Expires Feb 8, 2027.

## Content

### 3. Pin one sandboxed settings file to every Remote Control session — Enterprise feasibility: Medium | Stage: Trial
- What changes: sessions you start from your phone or claude.ai run under the same sandbox as your terminal, instead of whatever your user settings say.
- How it works: 2.1.321 added `claude remote-control --settings <file>`. If the file changes, no new session starts until you restart the server, so nobody can loosen it mid-run.
- Effort: ~5 min.
- PoC: save `rc-settings.json` as `{ "sandbox": { "enabled": true, "failIfUnavailable": true, "allowUnsandboxedCommands": false } }`, then run `claude remote-control --settings ./rc-settings.json`.
- Success metric: every remote session shows the sandbox on in `/status`.
- Sources: [v2.1.321 notes](https://github.com/anthropics/claude-code/releases/tag/v2.1.321), [sandboxing docs](https://code.claude.com/docs/en/sandboxing) | seen in 1 source | expires Feb 8, 2027

## Sources

- [v2.1.321 notes](https://github.com/anthropics/claude-code/releases/tag/v2.1.321)
- [sandboxing docs](https://code.claude.com/docs/en/sandboxing)
