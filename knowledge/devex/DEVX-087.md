# DEVX-087: Claude Code Code Mode (experimental): one JavaScript block runs many tool calls; trial on a personal account, then set an org policy (audit log + kill switch)

## Summary

Experimental opt-in (2.1.323+): Claude writes one JavaScript block that runs several tool calls (parallel, chained, filtered) and reads back only the result, aimed at repetitive multi-file edits and searches that need filtering. Not available with ZDR, HIPAA config, gateways, Bedrock, Claude Platform on AWS, Google Cloud's Agent Platform, Microsoft Foundry, or with OpenTelemetry export / DISABLE_TELEMETRY on; interactive terminal only. In auto mode the classifier reviews the code, not each call; deny/ask rules and PreToolUse hooks still apply per call. Since 2.1.329 a crashing PreToolUse hook no longer blocks a script's tool call, so add "onFailure": "block" to security hooks and consider asking before each script. Feasibility Medium, stage Assess, ~10 min.

## Details

- PoC: `CLAUDE_CODE_EXPERIMENTAL_CODE_MODE=1 claude`, then ask e.g. "Read every Markdown file in this project and list the links that point to local files that don't exist." Ctrl+O and expand a "Code" row to see the JavaScript it ran.
- Success metric: tokens and turns per multi-file task, Code Mode vs normal, on the same 3 tasks (`/cost`). Per @me_deepu, the circulating "37% fewer tokens" figure comes from Anthropic's API test of programmatic tool calling, not from Claude Code.
- Mod, Code Mode audit log (~3 min, needs `jq`; a hook that fails to start blocks the call, so check `which jq`): in `~/.claude/settings.json` add a `PreToolUse` hook with matcher `REPL` running `jq -c '{ts: (now|todate), session: .session_id, code: .tool_input.code}' >> ~/.claude/code-mode-audit.jsonl` (full JSON below; the command is an adaptation of the docs).
- Mod, org kill switch (~2 min): in `managed-settings.json` `{ "env": { "CLAUDE_CODE_EXPERIMENTAL_CODE_MODE": "0" } }`; managed 0 wins over a user's 1, running sessions keep it until restart. A project's settings can't turn it on.
- Most-discussed change on X this week (top post ~700 likes). Seen in 5+ sources. Expires Feb 13, 2027.

Update (Nov 22): 2.1.329: a `PreToolUse` hook that crashes no longer blocks a Code Mode script's tool call; add `"onFailure": "block"` to every security hook. Code Mode can now also start with telemetry off; keep managed `CLAUDE_CODE_EXPERIMENTAL_CODE_MODE=0` if you need it off. Mod: `{"permissions":{"ask":["REPL"]}}` to approve each script. See DEVX-098.

## Content

### 3. Code Mode: try it on a personal account, then set an org policy — Enterprise feasibility: Medium | Stage: Assess

- What changed: an experimental opt-in (2.1.323+) where Claude writes one JavaScript block that runs several tool calls (in parallel, chained, filtered) and reads back only the result. It's aimed at repetitive edits across many files and searches that need filtering. It was the most-discussed change on X this week (the top post had about 700 likes).
- Enterprise caveats: it isn't available with ZDR, the HIPAA configuration, gateways, Amazon Bedrock, Claude Platform on AWS, Google Cloud's Agent Platform or Microsoft Foundry, or with OpenTelemetry export or `DISABLE_TELEMETRY` on. It only runs in the interactive terminal. In auto mode the classifier reviews the code, not each call, and can't see values computed at run time. Your `deny`/`ask` rules and `PreToolUse` hooks still apply to every call. A project's settings can't turn it on, and managed settings can block it (see the mods below).
- Effort: ~10 min.
- PoC:

```bash
CLAUDE_CODE_EXPERIMENTAL_CODE_MODE=1 claude
# then: "Read every Markdown file in this project and list the links that point to local files that don't exist."
# Ctrl+O and expand a "Code" row to see the JavaScript it ran
```

- Success metric: tokens and turns per multi-file task, Code Mode vs normal, on the same 3 tasks (`/cost`). Don't count on the "37% fewer tokens" figure going around: per [@me_deepu](https://x.com/me_deepu/status/2121843228752417148), it comes from Anthropic's API test of programmatic tool calling, not from Claude Code.
- Sources: [Code Mode docs](https://code.claude.com/docs/en/code-mode), [2.1.323 release notes](https://github.com/anthropics/claude-code/releases/tag/v2.1.323), X posts by [@alexmichael](https://x.com/alexmichael/status/2121003637371470145), [@voidfreud](https://x.com/voidfreud/status/2121293579104751894) and [@aloft_ai](https://x.com/aloft_ai/status/2121573745261191666) | seen in 5+ sources | expires Feb 13, 2027

### Ready-to-use mods

- [Code Mode audit log (Claude Code)](https://code.claude.com/docs/en/code-mode#permission-checks): saves every JavaScript block Claude runs in Code Mode, so you can review it later. The docs say to match the `REPL` tool and read `tool_input.code`. ~3 min, needs `jq`. In Code Mode a hook that fails to start (exit 127) blocks the call, so check `which jq` first. In `~/.claude/settings.json`:

```json
{ "hooks": { "PreToolUse": [ { "matcher": "REPL", "hooks": [ { "type": "command",
  "command": "jq -c '{ts: (now|todate), session: .session_id, code: .tool_input.code}' >> ~/.claude/code-mode-audit.jsonl" } ] } ] } }
```

- [Org kill switch for Code Mode](https://code.claude.com/docs/en/code-mode#block-code-mode-for-your-organization): for regulated teams that haven't reviewed it yet. A `0` in managed settings wins over any user's `1`. Sessions already running keep it until they restart. ~2 min. In `managed-settings.json`:

```json
{ "env": { "CLAUDE_CODE_EXPERIMENTAL_CODE_MODE": "0" } }
```

Credit: both mods come from Anthropic's Code Mode docs and release notes. The audit-log command is an adaptation of the docs' `REPL` hook guidance.

### Nov 22 update: Claude Code 2.1.329

- **Hook failures:** a `PreToolUse` hook that crashes no longer blocks a Code Mode script's tool call. Add `"onFailure": "block"` to every security hook. Credit: [2.1.329 release](https://github.com/anthropics/claude-code/releases/tag/v2.1.329).
- **Telemetry:** Code Mode can now also start with telemetry off, so keep the managed `CLAUDE_CODE_EXPERIMENTAL_CODE_MODE=0` (the kill switch above) if you need it off.
- **Mod, approve each Code Mode script before it runs** (~2 min): this closes the gap left by the 2.1.329 hook change. Press `Ctrl+O` to read the code. Add to `~/.claude/settings.json`:

```json
{"permissions":{"ask":["REPL"]}}
```

See DEVX-098 for the full 2.1.329/2.1.330 alert.

## Sources

- [Code Mode docs](https://code.claude.com/docs/en/code-mode)
- [2.1.323 release notes](https://github.com/anthropics/claude-code/releases/tag/v2.1.323)
- [@alexmichael on X](https://x.com/alexmichael/status/2121003637371470145)
- [@voidfreud on X](https://x.com/voidfreud/status/2121293579104751894)
- [@aloft_ai on X](https://x.com/aloft_ai/status/2121573745261191666)
- [@me_deepu on X](https://x.com/me_deepu/status/2121843228752417148)
- [2.1.329 release notes](https://github.com/anthropics/claude-code/releases/tag/v2.1.329)
