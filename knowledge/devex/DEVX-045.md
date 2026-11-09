# DEVX-045: policy-ceiling mod: managed settings as ceilings/floors instead of fixed values

## Summary

claude-code-templates enterprise mod: users keep their own values inside org limits (max retention, denied models with fallback, max effort, forbidden permission modes, forced sandbox), with a /policy pane showing requested vs effective values.

## Details

Works only as a managed plugin in the prepend tier; rules read from the managed layer only, so user pluginConfigs can't loosen it. Doesn't cap --model, --permission-mode, Shift+Tab or /model: pair with the availableModels managed setting. Needs Claude Code 2.1.304+ (author verified on 2.1.316). Merged Nov 3 in PR #1366; untested by the agent. Snippet (managed-settings.json, from README): extraKnownMarketplaces {acme-tools: github acme/claude-plugins}; enabledPlugins {policy-ceiling@acme-tools: true}; prependPlugins [policy-ceiling@acme-tools, sec-default@builtin]; pluginConfigs policy-ceiling options {maxCleanupPeriodDays: 30, deniedModels: 'opus[1m]', fallbackModel: 'sonnet', maxEffort: 'high', forbiddenModes: 'bypassPermissions', requireSandbox: true}.

## Sources

- [policy-ceiling mod (claude-code-templates)](https://github.com/davila7/claude-code-templates/tree/main/cli-tool/components/mods/enterprise/policy-ceiling)
