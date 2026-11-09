# DEVX-032: Lock down who can edit Claude Code managed settings

## Summary

Since Claude Code 2.1.316, server-managed settings (incl. hooks and apiKeyHelper) apply for Team/Enterprise with no approval prompt, so a console editor can silently push a hook to every machine.

## Content

### Lock down who can edit Claude Code managed settings — Enterprise feasibility: High | Stage: Adopt
- **What changed:** Since 2.1.316, anyone who can edit managed settings in the admin console can silently push a hook to every developer machine.
- **Effort:** about 20 min.
- **PoC:** Review who holds that role and require SSO and MFA for it. Have a second person review each change, and test it on one machine with `claude doctor` (check the "Managed settings (remote)" line). Keep hooks and `apiKeyHelper` in MDM-managed settings.
- **Success metric:** a named, MFA-protected list of editors, and every change reviewed and tested before it reaches the fleet.
- **Sources:** [v2.1.316 release](https://github.com/anthropics/claude-code/releases/tag/v2.1.316), [server-managed settings docs](https://code.claude.com/docs/en/server-managed-settings#security-approval-dialogs). Expires Jan 30, 2027.

## Sources

- [v2.1.316 release](https://github.com/anthropics/claude-code/releases/tag/v2.1.316)
- [server-managed settings docs](https://code.claude.com/docs/en/server-managed-settings#security-approval-dialogs)
