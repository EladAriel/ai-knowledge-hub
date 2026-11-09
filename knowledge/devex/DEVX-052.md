# DEVX-052: Mod: fleet-wide plugin block plus custom plugin trust message (Claude Code managed settings)

## Summary

Managed enabledPlugins false blocks a plugin at every scope and hides it from the marketplace listing, even from the official marketplace where strictKnownMarketplaces can't help; pluginTrustMessage adds your org's line to the warning before any plugin install.

## Details

managed-settings.json: {"enabledPlugins": {"postman@claude-plugins-official": false}, "pluginTrustMessage": "All plugins from our marketplace are approved by IT"}. The pluginTrustMessage line is verbatim from Anthropic's settings reference; the false entry follows the plugins/org docs pattern. Untested.

## Sources

- [Claude Code plugins/org docs](https://code.claude.com/docs/en/plugins/org)
