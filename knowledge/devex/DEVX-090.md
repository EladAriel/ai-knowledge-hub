# DEVX-090: Pin the starting permission mode in managed settings

## Summary

Since 2.1.326, HIPAA-configured orgs start in auto mode. Any session with no mode set also starts in auto if the org policy hasn't loaded. `permissions.defaultMode` in managed settings outranks user and project settings. `disableAutoMode: "disable"` removes auto mode entirely. Putting these in the file-based managed settings (MDM) means they don't depend on a policy download. Since 2.1.328 (Nov 19), auto mode also starts by default on Bedrock, Google Agent Platform, Foundry and the Claude apps gateway. Enterprise feasibility: High. Stage: Adopt. Effort: about 5 minutes.

## Details

Practical PoC in `/etc/claude-code/managed-settings.json`. Use only `defaultMode` if people may still switch to auto:

```json
{ "permissions": { "defaultMode": "default", "disableAutoMode": "disable" } }
```

Success metric: new sessions show manual mode on, and `/status` lists the managed settings source. Seen in 3 sources. Expires Feb 16, 2027.

For wrappers that launch Claude Code headless or unattended, the same start-mode change means: always pass `--permission-mode` explicitly, and have a preflight check fail an unattended run that has no mode set.

Update Nov 19: Claude Code 2.1.328 extends the default: auto mode now starts by default on Bedrock, Google Agent Platform, Foundry and the Claude apps gateway (Opus/Sonnet 4.6, when no permission mode is set). If you want a fixed mode, set `defaultMode`/`disableAutoMode` in managed settings (same snippet as above). See DEVX-096.

## Content

- **Claude Code 2.1.328 (Nov 19): auto mode now starts by default on Bedrock, Google Agent Platform, Foundry and the Claude apps gateway** (Opus/Sonnet 4.6, when no permission mode is set). If you want a fixed mode, set `defaultMode`/`disableAutoMode` in managed settings (same snippet as above). [Release](https://github.com/anthropics/claude-code/releases/tag/v2.1.328)

## Sources

- [2.1.326 notes](https://github.com/anthropics/claude-code/releases/tag/v2.1.326)
- [permission modes: HIPAA](https://code.claude.com/docs/en/permission-modes#permission-modes-with-the-hipaa-configuration)
- [settings reference: disableAutoMode](https://code.claude.com/docs/en/settings-reference#disableautomode)
- [2.1.328 release notes](https://github.com/anthropics/claude-code/releases/tag/v2.1.328)
