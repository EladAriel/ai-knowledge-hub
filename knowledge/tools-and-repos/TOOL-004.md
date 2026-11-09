# TOOL-004: protect-mcp starter policy hook

## Summary

Built-in starter policy blocks force-pushing to main, 'rm -rf /', reading secrets, and 'curl | sh', with signed receipts.

## Content

**[protect-mcp](https://www.npmjs.com/package/protect-mcp) starter policy hook.** Its built-in starter policy blocks force-pushing to main, `rm -rf /`, reading secrets, and `curl | sh`, and it keeps signed receipts. With `onFailure: "block"`, it also blocks if the check itself fails. Use version 0.31.0 or later. **Effort:** ~15 min
```bash
npx protect-mcp@0.31.1 init --starter
```
```json
{"hooks":{"PreToolUse":[{"matcher":"","hooks":[{"type":"command","command":"npx protect-mcp@0.31.1 evaluate --policy builtin:starter --format claude","onFailure":"block"}]}]}}
```

r/ClaudeAI and X didn't return results this run, so nothing from them is included.

## Sources

- [protect-mcp](https://www.npmjs.com/package/protect-mcp)
