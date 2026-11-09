# DEVX-050: Claude Code 2.1.318: expiring logins visible to CI (loginExpiresAt, credential_expires_at, 10-day warning)

## Summary

claude auth status shows loginExpiresAt, claude -p JSON results carry credential_expires_at, and -p text output warns on stderr 10 days before the stored claude.ai login ends; config writes on shared/NFS homes now fail loudly instead of reporting success.

## Details

Fixes: /logout, claude auth logout and claude mcp remove no longer report success while changes are dropped on shared network homes; claude mcp add/remove take the config lock or exit 1; 'Not logged in' when another host re-signed in on a shared home; full network home could replace the stored login with an empty file; setup-token tokens refused under forceLoginOrgUUID; unattended runs no longer rewrite ~/.claude.json every run; assume_role on gateway mantle upstreams for per-developer AWS cost attribution.

## Sources

- [Claude Code v2.1.318 release](https://github.com/anthropics/claude-code/releases/tag/v2.1.318)
- [CHANGELOG](https://raw.githubusercontent.com/anthropics/claude-code/main/CHANGELOG.md)
