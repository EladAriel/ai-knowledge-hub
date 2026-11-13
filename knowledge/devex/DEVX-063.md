# DEVX-063: Cursor Live Apps: review admin controls before anyone publishes an internal tool

## Summary

Cursor's Nov 5 changelog: cloud agents can scaffold, host and publish apps behind Cursor SSO, optionally with Postgres (paid plans with cloud agents). Admins should set Apps on/off, public sharing, API-key access and custom review rules first, since this is a new shadow-IT surface.

## Details

Publish runs four always-on checks (block secrets in app files, block credential files, never publish .env or source maps) plus an AI security review. Admins can add review-prompt rules but can't remove built-in checks; can see every app and secret, unpublish, turn Apps on/off, allow/disallow public apps (off by default for Teams and Enterprise), allow/disallow API-key access; changes are audit-logged. Also noted: Cursor Voice Chat with Agents (Nov 6; Grok Voice; Privacy Mode uses zero data retention), lower leverage.
PoC: admin page cursor.com/dashboard/apps; curl -H "x-cursor-app-token: $CURSOR_API_KEY" https://\<your-app-url>; try only via a cloud agent, saying explicitly you want an app.
Success metric: admins reviewed Apps on/off, public sharing, API-key and custom review settings; no unexpected public apps.
Feasibility Medium, stage Assess; seen in 3 sources.

## Content

### 5. Review Cursor Live Apps admin controls before anyone publishes an internal tool — Enterprise feasibility: Medium | Stage: Assess
- **What changed:** [changelog](https://cursor.com/changelog) dated Nov 5 (not covered in the Thursday notes). Cloud agents can scaffold, host, and publish apps behind Cursor SSO, optionally with Postgres. Available on paid plans with cloud agents. Cursor also shipped Voice Chat with Agents on Nov 6 (Grok Voice; Privacy Mode uses zero data retention) — lower leverage than Live Apps, noted only so the changelog is covered.
- **How it works:** publish runs four always-on checks (block secrets in app files, block credential files, never publish `.env` or source maps) plus an AI security review. Admins can add review-prompt rules but cannot remove built-in checks, see every app and secret, unpublish, turn Apps on or off, allow or disallow public apps (off by default for Teams and Enterprise), and allow or disallow API-key access. Changes are audit-logged.
- **Effort:** ~20 min
- **PoC:**
```bash
# Admin first: https://cursor.com/dashboard/apps
# Docs: “Public sharing is disabled by default for Teams and Enterprise.”
curl -H "x-cursor-app-token: $CURSOR_API_KEY" https://<your-app-url>
# Try only via a cloud agent, saying explicitly that you want an app.
```
- **Success metric:** admins have reviewed Apps on/off, public-sharing, API-key, and custom review settings; no unexpected public apps.
- **Org challenge:** anyone with cloud agents can publish internal tools — a new shadow-IT surface until policy is set.
- **Sources:** [changelog](https://cursor.com/changelog), [Apps docs](https://cursor.com/docs/cloud-agent/apps), [dashboard](https://cursor.com/dashboard/apps) | seen in 3 sources

## Sources

- [Cursor changelog](https://cursor.com/changelog)
- [Cursor Apps docs](https://cursor.com/docs/cloud-agent/apps)
- [Cursor Apps dashboard](https://cursor.com/dashboard/apps)
