# DEVX-042: Claude Code 2.1.317 governance additions (email-send ask, OTel seat/plan attributes, cost API)

## Summary

Upgrade-only wins: asks before a web/shell call sends your account email, new OTel attributes for chargeback and shadow-gateway detection, gateway cost-report API, managed-settings load notice, /schedule connector warning.

## Details

Changes: (a) asks before a web or shell tool call sends the account email to the network (first built-in mitigation for issue #81138; the email is still in the prompt). (b) OTel attributes anthropic.plan, anthropic.seat_type, anthropic.provider, anthropic.custom_base_url on metrics, events, spans. (c) Claude apps gateway admin API GET /v1/organizations/analytics/cost (spend total, per developer, per day or per IdP group). (d) Desktop Code-tab notice when org remote managed settings haven't loaded. (e) /schedule warning when a cloud task gets connectors you didn't ask for. (f) onFailure 'block' now also for Agent SDK hook callbacks. (g) OTel export timeout 10 s, up to 30 s via OTEL_EXPORTER_OTLP_TIMEOUT. PoC: npm view @anthropic-ai/claude-code dist-tags; roll fleet to >= 2.1.317; in the OTel backend group by anthropic.seat_type / anthropic.plan, filter anthropic.custom_base_url != '' for unsanctioned gateways; on self-hosted runners relying on nested -p export CLAUDE_CODE_DISABLE_NESTED_SESSION_ID=1. Success metric: 100% of seats on >= 2.1.317 within a week, one OTel panel by seat_type, 0 unexpected custom_base_url. Caveats: not in docs yet (confirm field names on real data); stable channel is 2.1.311, so the email ask only reaches 'latest' fleets for now. Enterprise feasibility High, stage Adopt.

## Content

**[Claude Code 2.1.317 governance additions: asks before sending your account email to the network, OTel plan/seat/provider/base-URL attributes, gateway cost-report API, and a notice when managed settings haven't loaded](https://github.com/anthropics/claude-code/releases/tag/v2.1.317)**
- **urls_extra:** ["https://raw.githubusercontent.com/anthropics/claude-code/main/CHANGELOG.md", "https://code.claude.com/docs/en/changelog", "https://github.com/anthropics/claude-code/issues/81138", "https://dev.to/piekwerk/claude-code-21317-tightens-failure-defaults-sdk-hook-callbacks-can-block-and-an-email-leak-now-768", "https://claudeworld.news/claude-code/claude-code-v2-1-317-ekm7gekkpe64", "https://x.com/sunset_evm/status/2117518927949451379"]
- **what_changed:** Enterprise-relevant lines  SDK hook callbacks; command and http hooks have had it since 2.1.295, reported Oct 10. (g) OTel exports behind a proxy that never answers now time out after 10 s, configurable up to 30 s with `OTEL_EXPORTER_OTLP_TIMEOUT`. Docs lag: env-vars, monitoring-usage and the gateway pages don't list the new OTel attributes, the cost endpoint or `CLAUDE_CODE_DISABLE_NESTED_SESSION_ID` yet (checked Nov 3).
- **how_it_works:** The email check is a client-side ask on web and shell tool calls that would carry the account email. The OTel attributes ride on every existing metric, event and span, so if you already export OTel, you can split cost and usage by plan and seat type with no new pipeline. `anthropic.custom_base_url` also shows sessions routed through a non-Anthropic base URL (shadow gateways or proxies). The cost report is an admin API on the self-hosted Claude apps gateway.
- **enterprise_feasibility:** High
- **stage:** Adopt
- **effort_minutes:** 20
- **poc_snippet:** # my composition (standard commands), not from the changelog
npm view @anthropic-ai/claude-code dist-tags      # expect latest 2.1.317, stable 2.1.311
claude --version                                  # roll the fleet to >= 2.1.317 for the email ask

# in your OTel backend, after upgrade: group existing claude_code metrics by the new attributes
#   group by anthropic.seat_type, anthropic.plan      -> chargeback / seat right-sizing
#   filter anthropic.custom_base_url != ''             -> sessions on an unsanctioned gateway/proxy

# self-hosted runners that relied on nested -p sharing the parent session:
export CLAUDE_CODE_DISABLE_NESTED_SESSION_ID=1
- **success_metric:** 100% of seats on >= 2.1.317 within a week. One OTel dashboard panel by seat_type. 0 sessions with an unexpected anthropic.custom_base_url.
- **org_challenge_if_relevant:** The new attributes and the cost endpoint aren't in the docs yet, so field names should be confirmed against real exported data before you build dashboards. The stable channel is now 2.1.311, so the email ask only reaches fleets on `latest` until stable catches up.
- **project_health_if_relevant:** Official Anthropic release. Three independent write-ups (dev.to, claudeworld.news, labmemo.com) and X posts appeared within hours.
- **source_count:** 5
- **benefit_to_effort:** High
- **why_enterprise_simple:** An upgrade, with no config needed, gives a PII-exfil prompt, seat-level cost attribution in the OTel you already have, and visibility of managed-settings load failures.

## Sources

- [Claude Code v2.1.317 release](https://github.com/anthropics/claude-code/releases/tag/v2.1.317)
- [Issue #81138 (email in prompt)](https://github.com/anthropics/claude-code/issues/81138)