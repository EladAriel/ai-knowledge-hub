# DEVX-061: Keep Claude Code's built-in privacy mod on, but it doesn't cover WebFetch, WebSearch, MCP or general email exfil

## Summary

Issue #107757 (Nov 6) reports the account email leaving via User-Agent during web searches on 2.1.318. On 2.1.317+ the built-in cc-plugin-privacy (default on) is a tool.check hook that refuses Bash/PowerShell/Monitor input holding the signed-in address and naming a User-Agent; its own README calls it 'a courtesy, not a boundary'. Keep it on and keep an extra never-send hook for the uncovered surfaces.

## Details

Background: distinct from #81138 (email in the system prompt) but linked: the model is given the account email and sometimes put it in a User-Agent when a site asked for a contact. Anthropic said they will drop the email from model context in a later release; not in the 2.1.319 changelog. The official privacy mod README is now public.
Documented gaps: address with no User-Agent named (URL, body, curl -u, From:); WebFetch, WebSearch and MCP tools are not checked; computed, variable, file or script encodings pass. Disable path: /plugin disable or "cc-plugin-privacy@builtin": false in user / --settings / managed settings (not repository settings). Stable 2.1.311 does not have this default.
PoC: grep -n 'cc-plugin-privacy' ~/.claude/settings.json /etc/claude-code/managed-settings.json; confirm it is listed builtin/enabled in /plugins; do not ship the disable setting.
Success metric: no fleet settings file disables it; security review records that WebFetch/WebSearch/MCP are outside it; an additional never-send hook stays in place for those surfaces.
Feasibility High, stage Adopt; seen in 6 sources. Related: the earlier DevEx item 'PreToolUse hook: block your email from going out in tool calls' (Nov 1).

## Content

### 3. Keep the built-in privacy mod on, but do not treat it as covering WebFetch, WebSearch, or a general email-exfil boundary — Enterprise feasibility: High | Stage: Adopt
- **What changed:** [#107757](https://github.com/anthropics/claude-code/issues/107757) (opened Nov 6 at 00:13 Israel time; [HN 50385272](https://news.ycombinator.com/item?id=50385272)) reports the account email leaving via `User-Agent` during web searches on 2.1.318. Distinct from already-reported #81138 (email in the system prompt), but linked: the model was given the account email and sometimes put it in a User-Agent when a site asked for a contact. Anthropic said they will drop the email from model context in a later release; that change is not in the 2.1.319 changelog. The official [privacy mod README](https://github.com/anthropics/claude-code/tree/main/mods/privacy) is now public.
- **How it works:** on 2.1.317+ the built-in `cc-plugin-privacy` (default on) is a `tool.check` hook that refuses Bash/PowerShell/Monitor input that both holds the signed-in address and names a User-Agent, with no prompt, in every permission mode. Documented gaps: the address with no User-Agent named (URL, body, `curl -u`, `From:`); WebFetch, WebSearch, and MCP tools are not checked; computed, variable, file, or script encodings pass. The README calls it “a courtesy, not a boundary.” Disable path: `/plugin disable` or `"cc-plugin-privacy@builtin": false` in user/`--settings`/managed settings (not repository settings). Stable is still 2.1.311, which does not have this default.
- **Effort:** ~10 min
- **PoC:**
```bash
# Official disable path — do NOT ship this if you want the default on
# { "enabledPlugins": { "cc-plugin-privacy@builtin": false } }
grep -n 'cc-plugin-privacy' ~/.claude/settings.json /etc/claude-code/managed-settings.json 2>/dev/null
# Confirm it is listed builtin/enabled in /plugins.
```
- **Success metric:** no fleet settings file sets `cc-plugin-privacy@builtin` to false; security review records that WebFetch/WebSearch/MCP are outside this mod; any additional never-send hook remains in place for those surfaces.
- **Sources:** [#107757](https://github.com/anthropics/claude-code/issues/107757), [privacy README](https://raw.githubusercontent.com/anthropics/claude-code/main/mods/privacy/README.md), [HN 50385272](https://news.ycombinator.com/item?id=50385272), [privacy mod tree](https://github.com/anthropics/claude-code/tree/main/mods/privacy) | seen in 6 sources

## Sources

- [#107757](https://github.com/anthropics/claude-code/issues/107757)
- [privacy README](https://raw.githubusercontent.com/anthropics/claude-code/main/mods/privacy/README.md)
- [HN 50385272](https://news.ycombinator.com/item?id=50385272)
- [privacy mod tree](https://github.com/anthropics/claude-code/tree/main/mods/privacy)
