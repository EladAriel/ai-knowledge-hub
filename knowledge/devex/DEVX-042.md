# DEVX-042: Claude Code 2.1.317 governance additions (email-send ask, OTel seat/plan attributes, cost API)

## Summary

Upgrade-only wins: asks before a web/shell call sends your account email, new OTel attributes for chargeback and shadow-gateway detection, gateway cost-report API, managed-settings load notice, /schedule connector warning.

## Details

Changes: (a) asks before a web or shell tool call sends the account email to the network (first built-in mitigation for issue #81138; the email is still in the prompt). (b) OTel attributes anthropic.plan, anthropic.seat_type, anthropic.provider, anthropic.custom_base_url on metrics, events, spans. (c) Claude apps gateway admin API GET /v1/organizations/analytics/cost (spend total, per developer, per day or per IdP group). (d) Desktop Code-tab notice when org remote managed settings haven't loaded. (e) /schedule warning when a cloud task gets connectors you didn't ask for. (f) onFailure 'block' now also for Agent SDK hook callbacks.

## Sources

- [Claude Code v2.1.317 release](https://github.com/anthropics/claude-code/releases/tag/v2.1.317)
- [Issue #81138 (email in prompt)](https://github.com/anthropics/claude-code/issues/81138)
