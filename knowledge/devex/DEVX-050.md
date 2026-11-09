# DEVX-050: Claude Code 2.1.318: expiring logins visible to CI (loginExpiresAt, credential_expires_at, 10-day warning)

## Summary

claude auth status shows loginExpiresAt, claude -p JSON results carry credential_expires_at, and -p text output warns on stderr 10 days before the stored claude.ai login ends; config writes on shared/NFS homes now fail loudly instead of reporting success.

## Details

Fixes: /logout, claude auth logout and claude mcp remove no longer report success while changes are dropped on shared network homes; claude mcp add/remove take the config lock or exit 1; 'Not logged in' when another host re-signed in on a shared home; full network home could replace the stored login with an empty file; setup-token tokens refused under forceLoginOrgUUID; unattended runs no longer rewrite ~/.claude.json every run; assume_role on gateway mantle upstreams for per-developer AWS cost attribution. PoC: npm view @anthropic-ai/claude-code dist-tags; claude auth status; claude -p 'echo ok' --output-format json | jq -r '.credential_expires_at' (check the JSON shape on your build). Success metric: 0 scheduled jobs failing on expired logins; alerts at least 7 days ahead. Caveat: only on latest until stable moves past 2.1.311; long-lived runners should prefer setup-token/API keys. Feasibility High, stage Trial.

## Content

**[Claude Code 2.1.318 makes expiring logins visible to CI (`loginExpiresAt`, `credential_expires_at`, a 10-day stderr warning) and makes shared-home and NFS config writes fail loudly](https://github.com/anthropics/claude-code/releases/tag/v2.1.318)**
- **urls_extra:** ["https://raw.githubusercontent.com/anthropics/claude-code/main/CHANGELOG.md", "https://x.com/alexmichael/status/2117781675157422208", "https://x.com/automatethebs/status/2117824657495855213", "https://x.com/VasilisTsolis/status/2117883245828210779"]
- **what_changed:** Added: the date a stored claude.ai sign-in ends, in `claude auth status` (`loginExpiresAt`) and in `claude -p` JSON results (`credential_expires_at`), plus a one-line stderr warning in `claude -p` text output starting 10 days before the sign-in ends. Expired logins in -p now name `claude auth login` and `claude setup-token`. Fixed: `/logout`, `claude auth logout` and `claude mcp remove` reported success while trust, consent or MCP changes were silently dropped on shared network homes. `claude mcp add`/`remove` now take the config lock, or exit 1. Jobs exited `Not logged in` when another host re-signed in to the same account on a shared home. A full network home could replace the stored login with an empty file. `setup-token` tokens were refused under `forceLoginOrgUUID`. Unattended runs no longer rewrite `~/.claude.json` on every run. Also: `assume_role` on gateway `mantle` upstreams for per-developer AWS cost attribution.
- **how_it_works:** CI reads the new JSON field, or `claude auth status`, and alerts or rotates before the stored claude.ai login lapses, rather than finding out from a failed nightly job.
- **enterprise_feasibility:** High
- **stage:** Adopt
- **effort_minutes:** 20
- **poc_snippet:** # my composition around the documented fields (check the exact JSON shape on your build)
npm view @anthropic-ai/claude-code dist-tags     # latest 2.1.318, stable 2.1.311
claude auth status                               # look for loginExpiresAt
# CI step: fail early and page the owner if the -p result carries an expiry within 10 days
claude -p 'echo ok' --output-format json | jq -r '.credential_expires_at'
- **success_metric:** 0 scheduled jobs failing on expired claude.ai logins. Expiry alerts fire at least 7 days ahead.
- **org_challenge_if_relevant:** Only fleets on `latest` get this until npm `stable` (2.1.311) moves. Long-lived runners should prefer `setup-token`/API keys over a person's claude.ai login anyway.
- **project_health_if_relevant:** Official release with 84 changelog lines. 10+ independent X write-ups within hours.
- **source_count:** 4
- **benefit_to_effort:** High
- **why_enterprise_simple:** An upgrade plus one jq line turns silent CI auth expiry into an early warning.

## Sources

- [Claude Code v2.1.318 release](https://github.com/anthropics/claude-code/releases/tag/v2.1.318)
- [CHANGELOG](https://raw.githubusercontent.com/anthropics/claude-code/main/CHANGELOG.md)