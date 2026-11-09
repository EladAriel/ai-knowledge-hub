# DEVX-032: Lock down who can edit Claude Code managed settings

## Summary

Since Claude Code 2.1.316, server-managed settings (incl. hooks and apiKeyHelper) apply for Team/Enterprise with no approval prompt, so a console editor can silently push a hook to every machine.

## Details

Review who holds the role and require SSO + MFA; second-person review for each change; test on one machine with claude doctor ('Managed settings (remote)' line). Keep hooks and apiKeyHelper in MDM-managed settings. Success: named MFA-protected editor list, every change reviewed and tested before fleet. Stage Adopt.

## Sources

- [v2.1.316 release](https://github.com/anthropics/claude-code/releases/tag/v2.1.316)
- [server-managed settings docs](https://code.claude.com/docs/en/server-managed-settings#security-approval-dialogs)
