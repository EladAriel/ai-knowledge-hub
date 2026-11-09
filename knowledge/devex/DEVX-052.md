# DEVX-052: Mod: fleet-wide plugin block plus custom plugin trust message (Claude Code managed settings)

## Summary

Managed enabledPlugins false blocks a plugin at every scope and hides it from the marketplace listing, even from the official marketplace where strictKnownMarketplaces can't help; pluginTrustMessage adds your org's line to the warning before any plugin install.

## Details

managed-settings.json: {"enabledPlugins": {"postman@claude-plugins-official": false}, "pluginTrustMessage": "All plugins from our marketplace are approved by IT"}. The pluginTrustMessage line is verbatim from Anthropic's settings reference; the false entry follows the plugins/org docs pattern. Untested.

## Content

**[Block one named plugin fleet-wide, plus a custom trust-warning line (Claude Code managed settings)](https://code.claude.com/docs/en/plugins/org)**
- **what_it_gives:** Answers today's Postman case directly. Managed `enabledPlugins: false` 'block[s] a plugin at every scope and hide[s] it from the marketplace listing', even from the official marketplace, where `strictKnownMarketplaces` can't help. `pluginTrustMessage` adds your org's text to the warning shown before any plugin install.
- **effort_minutes:** 10
- **snippet:** // managed-settings.json. pluginTrustMessage example is verbatim from settings-reference; the enabledPlugins false entry follows the plugins/org docs pattern
{
  "enabledPlugins": {
    "postman@claude-plugins-official": false
  },
  "pluginTrustMessage": "All plugins from our marketplace are approved by IT"
}
- **source_credit:** code.claude.com/docs/en/plugins/org ('Require a marketplace and its plugins' and the control matrix) and settings-reference#plugintrustmessage

## Sources

- [Claude Code plugins/org docs](https://code.claude.com/docs/en/plugins/org)