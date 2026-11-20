# DEVX-082: Pre-trust peek: print a cloned repo's agent config (hooks, .mcp.json, rules) before trusting the folder

## Summary

A repo's hooks and .mcp.json can run as soon as you trust the folder in Claude Code or Cursor, so print them first. A small shell function (agentpeek) dumps CLAUDE.md, AGENTS.md, CLAUDE.local.md, .mcp.json, .claude/settings.json, .cursor/mcp.json and lists .claude/agents|commands|skills and .cursor/rules. ~2 min.

## Details

Add the `agentpeek()` function to `~/.bashrc` or `~/.zshrc` (full one-liner below) and run it in a freshly cloned repo before opening an agent. Credit: idea from @VibeKitLab on X; the function is an adaptation of that idea.

## Content

### Ready-to-use mod: pre-trust peek for cloned repos

[Pre-trust peek for cloned repos](https://x.com/VibeKitLab/status/2120561709840769244): a repo's hooks and `.mcp.json` can run as soon as you trust the folder, so print them before you open Claude Code or Cursor. ~2 min. Add to `~/.bashrc` or `~/.zshrc`:

```bash
agentpeek() { for f in CLAUDE.md AGENTS.md CLAUDE.local.md .mcp.json .claude/settings.json .cursor/mcp.json; do [ -f "$f" ] && echo "=== $f" && cat "$f"; done; ls -R .claude/agents .claude/commands .claude/skills .cursor/rules 2>/dev/null; }
```

Credit: the peek idea is from @VibeKitLab on X, and the function is an adaptation of it.

## Sources

- [@VibeKitLab on X](https://x.com/VibeKitLab/status/2120561709840769244)
