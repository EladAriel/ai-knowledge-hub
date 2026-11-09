# DEVX-047: Postman Desktop silently installs its plugin/hook into Claude Code, Codex, Cursor, Copilot CLI: detect and block

## Summary

Postman desktop updates 12.33.4 and 12.35.1 installed postman@claude-plugins-official into Claude Code at user scope, a Codex marketplace/plugin plus a self-trusted SessionStart hook, a remote MCP entry (mcp.postman.com) and a CLI, without asking. A managed enabledPlugins false entry blocks it in Claude Code.

## Details

Evidence: issue #14370 (305 reactions), HN 1,202 points; Postman's own log records source 'auto-existing-upgrade' with claude-code:installed, codex:installed; second user on 12.35.1; Copilot entries in ~/.copilot/settings.json; installer function 'Approves only Postman's current hook after installation' (confirmed by The Proof Desk). Hook tells the agent to load postman:api-engineer before any non-trivial API task. Unverified: a reply in Postman's voice promising clearer opt-in (account not marked as Postman); the HN claim that all API data is shared isn't shown by the issue. Why it matters (AI methods): a new agent supply-chain vector where a legitimate app changes user-level agent config; recurring theme (Oct 25, 27, 28, 31). Marketplace allowlist (strictKnownMarketplaces) doesn't stop it because it's in the official marketplace. PoC: grep -n postman ~/.claude/settings.json ~/.claude/plugins/installed_plugins.json ~/.codex/config.toml ~/.copilot/settings.json; ls [local path removed] ~/.local/bin/postman; npx @postman/postman-plugin status / remove; managed-settings.json {"enabledPlugins": {"postman@claude-plugins-official": false}}. Success metric: 0 machines with an unapproved Postman plugin entry; managed block deployed and /plugin shows postman blocked. Org challenge: Codex, Cursor, Copilot CLI need their own controls; lasting control is managed enabledPlugins plus drift alerts on user-scope agent configs (or allowManagedHooksOnly / strictPluginOnlyCustomization). Don't trust trust records an app wrote itself. Feasibility High, stage Adopt. AI methods scores: effectiveness 4/5, hype 3/5. Nov 5 follow-up (DevEx): the issue is still open (~597 reactions); on Nov 5 at 05:46 Israel time a Postman MEMBER wrote they are reverting the auto-install and will redesign for clearer control. No desktop build or changelog confirming the revert was found yet, so keep the managed enabledPlugins false for postman@claude-plugins-official, re-check machines, and only drop the block after a known clean build. Already-installed plugins stay put; Codex/Cursor/Copilot need their own controls.

## Content

**[Postman desktop auto-installs its plugin into Claude Code, Codex, Cursor and Copilot CLI on existing users' machines (and approves its own Codex SessionStart hook). Check machines and block it with one managed-settings line](https://github.com/postmanlabs/postman-app-support/issues/14370)**
- **urls_extra:** ["https://news.ycombinator.com/item?id=50354960", "https://github.com/postmanlabs/postman-plugin", "https://code.claude.com/docs/en/plugins/org", "https://fourweekmba.com/ai-postman-users-say-app-auto-installed-claude-codex-plugins/", "https://sobolewski.pro/en/blog/postman-claude-code-plugin", "https://x.com/hackerlogs/status/2117729535491969194"]
- **what_changed:** Issue #14370 was opened Oct 25 and blew up Nov 3. The HN story was posted at 17:22Z (19:22 Israel time) and has 1,202 points and 392 comments; the issue has 305 reactions and 38 comments. Postman's own log on a Mac running 12.33.4 records `{"source":"auto-existing-upgrade","results":["claude-code:installed","codex:installed"]}`. The reported changes: `postman@claude-plugins-official` 2.0.1 enabled at user scope in `~/.claude/settings.json`; a Codex marketplace, plugin and `hooks.state` trusted_hash for Postman's SessionStart hook; a remote MCP entry for mcp.postman.com; and a Postman CLI in `~/.local/bin`. The hook tells the agent to load `postman:api-engineer` before 'any non-trivial API engineering task'. A second user hit the same path on 12.35.1 at Nov 3 22:58Z (00:58 Israel time, Nov 4), with `cursor:already-installed`. A third commenter found Postman entries in `~/.copilot/settings.json`. Postman's installer source has a function headed 'Approves only Postman's current hook after installation'. A reply written in Postman's voice (Nov 3 23:36Z, 01:36 Israel time; the account isn't marked as a Postman member) says the CLI and plugins are bundled on purpose and promises a clearer opt-in for existing users. No fix has shipped. The HN headline's claim that Postman 'attempts to share all API data' isn't shown by the issue's evidence, which explicitly doesn't claim exfiltration.
- **how_it_works:** A desktop app update runs an installer that writes into other tools' user-scope config. The plugin comes  (from its README).
- **enterprise_feasibility:** High
- **stage:** Adopt
- **effort_minutes:** 15
- **poc_snippet:** # 1) Check a dev machine (paths from the issue; my composition)
grep -n postman ~/.claude/settings.json ~/.claude/plugins/installed_plugins.json ~/.codex/config.toml ~/.copilot/settings.json 2>/dev/null
ls [local path removed] ~/.local/bin/postman 2>/dev/null
grep -h 'auto-existing-upgrade' ~/Library/Application\ Support/Postman/logs/main.log 2>/dev/null | tail -3

# 2) Undo it (Postman's README: 'status' shows, 'remove' uninstalls, '--agent <id>' limits to one agent)
npx @postman/postman-plugin status
npx @postman/postman-plugin remove

# 3) Block it fleet-wide in Claude Code: managed-settings.json (key documented at code.claude.com/docs/en/plugins/org)
{
  "enabledPlugins": { "postman@claude-plugins-official": false }
}
- **success_metric:** 0 machines with a Postman plugin entry that nobody approved. The managed block is deployed, and `/plugin` shows postman as blocked.
- **org_challenge_if_relevant:** Codex, Cursor and Copilot CLI need their own controls, and Claude Code's managed `false` only covers Claude Code. A vendor can ship the same pattern under another plugin name, so the lasting control is managed `enabledPlugins` plus watching for drift in user-scope agent configs (or `allowManagedHooksOnly` / `strictPluginOnlyCustomization`, both reported earlier).
- **project_health_if_relevant:** Vendor behavior, not a CVE. The reporter's evidence is detailed and reproduced by a second user on a newer build. The vendor promised changes, but none have landed.
- **source_count:** 6
- **benefit_to_effort:** Very high
- **why_enterprise_simple:** One grep finds it, one command removes it, and one managed-settings line stops it  config without asking.

**1. [Postman Desktop self-installed plugins for Claude Code and Codex](https://github.com/postmanlabs/postman-app-support/issues/14370)**
- **What is it:** An update of Postman Desktop installed without asking plugins for Claude Code and Codex. Along with them came a hook that runs at every start of a session, a remote MCP connection and a CLI. The hook instructs the agent to pass each API task through the Postman skill, and the installer reportedly also marked the hook as trusted.
- **Why new:** This is a new supply chain vector. A legitimate app modifies the user-level agent config on its own, without any malicious plugin.
- **Evidence:**
  - There are lines from Postman's own logs and two independent reporters. The second one reported on 3.11, on version 12.35.1.- [The Proof Desk](https://theproofdesk.com/postman-desktop-auto-installs-claude-code-codex-plugins-hook) Find the function in the installer code.
  - The HN discussion received 1,207 points.
  - **Not verified:** A response from the company promises a clearer opt-in, but it is not clear that the account really belongs to Postman. The claim in the HN title that "all API data is shared" was also not proven in the issue.
- **Scores:** Effectiveness 4/5, Hype 3/5.
- **Fit:** High for any agent product that loads hooks, skills or MCP from the disk. **low** effort:
  - enforce allowlist.
  - Alert on any change in the agent's config files.
  - Do not trust trust records that an application wrote itself.
- **Recommendation: Adopt** for controls. The theme repeats: supply chain and agent control also came up on October 25, 27, 28 and 31.

**URGENT, SECURITY:** Postman Desktop updates (version 12.33.4 and above) silently installed plugins for Claude Code, Codex, and Cursor. Along with them comes a SessionStart hook that marks itself as trusted and routes API tasks through the Postman skill. If you have Postman installed, check now what's added in `~/.claude` (plugins/hooks), `~/.codex` and `mcp.json` of Cursor. ([issue #14370](https://github.com/postmanlabs/postman-app-support/issues/14370))

From today's digests, two items passed the filter:

1. **gate for the integrity of the config of the agents (H-16):** Save a hash of the config files at the user level of Claude Code, Codex and Cursor. The `harness-preflight` refuses to run unattended if anything has changed since your last confirmation, until you reconfirm from TTY.
   - **Why this fits:** Your gates trust that the agent is running with the config you approved, and a legitimate app just proved it can change it without asking. It's the same principle as H-15, only on config instead of version.
   - **Effort:** Small, about 20 minutes.- **Source:** Same issue.
   - **in line for 9:00.**
2. **When you transfer context to a subagent, only the latest version of the spec and tickets are transferred.** According to the study, length almost does not affect the results, but a contradictory statement on the same fact (for example, an old spec to a new side) increases the error by 9 to 110 times. This is relevant to the problem of the context of your subagents.
   - **Effort:** Tiny.
   - **Source:** [Length Is Cheap, Competition Is Not](https://arxiv.org/abs/2611.04169). Note that only small open models were tested.

And Claude Code 2.1.318 came out tonight, so it's not worth upgrading before it passes the H-15 pin gate. One of the changes in it: if `~/.claude.json` is broken, headless runs fail instead of silently resetting it.

**[Postman MEMBER reply: they are reverting the auto-installation of agent plugins/hooks. Keep the managed block and re-check machines until a shipped build proves it](https://github.com/postmanlabs/postman-app-support/issues/14370#issuecomment-6649122696)**
- **urls_extra:** ["https://github.com/postmanlabs/postman-app-support/issues/14370", "https://code.claude.com/docs/en/plugins/org", "https://github.com/postmanlabs/postman-plugin"]- **what_changed:** Follow-up to the Nov 4 digest item. Issue #14370 is still open; reactions are now 597 (was ~305). On Nov 5 at 03:46Z (05:46 Israel time) GitHub user preethammavin posted with author_association MEMBER: they intended the desktop bundling to simplify setup, 'understand this wasn’t the case', will re-design for clearer control, and 'In the meantime, we are reverting this change.' An earlier non-MEMBER reply (yumeria, 01:40Z) promised clearer opt-in but was not a MEMBER. No new desktop version number or changelog entry confirming the revert has shipped was found in this lookback.
- **how_it_works:** Treat the MEMBER comment as intent, not as proof every machine is clean. Keep yesterday's managed enabledPlugins false for postman@claude-plugins-official, re-run the machine grep / npx @postman/postman-plugin status, and only drop the managed block after a known Postman build that no longer writes agent configs.
- **enterprise_feasibility:** High
- **stage:** Adopt
- **effort_minutes:** 15
- **poc_snippet:** # still the Nov 4 checklist; MEMBER said revert is coming, not that it already landed
grep -n postman ~/.claude/settings.json ~/.claude/plugins/installed_plugins.json ~/.codex/config.toml ~/.copilot/settings.json 2>/dev/null
npx @postman/postman-plugin status
# keep managed-settings.json until a build is verified clean:
# { "enabledPlugins": { "postman@claude-plugins-official": false } }
- **success_metric:** No new Postman plugin/hook writes after the next desktop update; managed block still present until then.
- **org_challenge_if_relevant:** A verbal revert can leave already-installed plugins in place. Codex/Cursor/Copilot controls are still separate from Claude Code's managed false.
- **project_health_if_relevant:** Official MEMBER reply on the vendor's own issue tracker; fix not yet verified in a release.
- **source_count:** 3
- **benefit_to_effort:** Very high
- **why_enterprise_simple:** Same 15-minute check as yesterday, now with an official signal that the vendor is pulling the behaviour back.

## Sources

- [Postman issue #14370](https://github.com/postmanlabs/postman-app-support/issues/14370)
- [HN thread](https://news.ycombinator.com/item?id=50354960)
- [postman-plugin README](https://github.com/postmanlabs/postman-plugin)
- [Claude Code plugins/org docs](https://code.claude.com/docs/en/plugins/org)
- [The Proof Desk](https://theproofdesk.com/postman-desktop-auto-installs-claude-code-codex-plugins-hook)
- [Postman MEMBER revert comment](https://github.com/postmanlabs/postman-app-support/issues/14370#issuecomment-6649122696)
- [Length Is Cheap, Competition Is Not](https://arxiv.org/abs/2611.04169)