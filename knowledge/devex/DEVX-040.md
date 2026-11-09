# DEVX-040: Alert (unconfirmed): claude.ai connectors expose no tools in headless claude -p

## Summary

Since ~22:00 Israel time Nov 1, Anthropic-hosted connectors (e.g. Microsoft 365) show Connected but expose no tools in -p sessions; interactive sessions and locally added HTTP MCP servers still work.

## Details

Single report, nothing changed client-side. If cron or CI jobs depend on those connectors, check last night's runs.

## Content

## Breaking-change alerts
- **Unconfirmed (one report): claude.ai connectors stopped loading in headless `claude -p` runs.** Since about 22:00 Israel time on Nov 1, connectors hosted by Anthropic, such as Microsoft 365, show as Connected but expose no tools in `-p` sessions. Interactive sessions and locally added HTTP MCP servers still work, and nothing changed on the client side. If any cron or CI jobs depend on those connectors, check last night's runs. ([issue #106630](https://github.com/anthropics/claude-code/issues/106630))

## Sources

- [issue #106630](https://github.com/anthropics/claude-code/issues/106630)