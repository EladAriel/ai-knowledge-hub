# DEVX-045: policy-ceiling mod: managed settings as ceilings/floors instead of fixed values

## Summary

claude-code-templates enterprise mod: users keep their own values inside org limits (max retention, denied models with fallback, max effort, forbidden permission modes, forced sandbox), with a /policy pane showing requested vs effective values.

## Content

**[policy-ceiling (claude-code-templates, enterprise): managed settings as ceilings/floors instead of fixed values (max retention, denied models plus fallback, max effort, forbidden permission modes, sandbox floor), with a /policy pane](https://github.com/davila7/claude-code-templates/tree/main/cli-tool/components/mods/enterprise/policy-ceiling)**
- **what_it_gives:** Normally a managed value overrides everyone (cleanupPeriodDays: 30 means exactly 30). This mod lets people keep their own value inside the org's limit: retention at most N days, `opus[1m]` mapped to a fallback model, effort capped at `high`, `bypassPermissions` turned back into `default`, and the sandbox forced on with no unsandboxed escape. `/policy` shows, for each key, what the person asked for, the limit and the effective value. It only works as a managed plugin in the prepend tier, and its rules are read from the managed layer only, so a user's pluginConfigs can't loosen it. It doesn't cap `--model`, `--permission-mode`, Shift+Tab or `/model`, so pair it with the `availableModels` managed setting. Needs Claude Code 2.1.304+, and the author verified it on 2.1.316. Merged Nov 3 at 03:20Z (05:20 Israel time) in PR #1366. New and untested here.
- **effort_minutes:** 30
- **snippet:** // managed-settings.json (macOS /Library/Application Support/ClaudeCode/, Linux /etc/claude-code/, or server-managed)
{
  "extraKnownMarketplaces": {
    "acme-tools": { "source": { "source": "github", "repo": "acme/claude-plugins" } }
  },
  "enabledPlugins": { "policy-ceiling@acme-tools": true },
  "prependPlugins": ["policy-ceiling@acme-tools", "sec-default@builtin"],
  "pluginConfigs": {
    "policy-ceiling@acme-tools": {
      "options": {
        "maxCleanupPeriodDays": 30,
        "deniedModels": "opus[1m]",
        "fallbackModel": "sonnet",
        "maxEffort": "high",
        "forbiddenModes": "bypassPermissions",
        "requireSandbox": true
      }
    }
  }
}

# get the files to copy into your org marketplace repo
npx claude-code-templates@latest --mod enterprise/policy-ceiling
- **source_credit:** davila7/claude-code-templates, cli-tool/components/mods/enterprise/policy-ceiling/README.md (Install section), PR #1366

## Sources

- [policy-ceiling mod (claude-code-templates)](https://github.com/davila7/claude-code-templates/tree/main/cli-tool/components/mods/enterprise/policy-ceiling)
