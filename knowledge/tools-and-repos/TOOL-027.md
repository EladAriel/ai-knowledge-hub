# TOOL-027: Grim Prompter /threat-model

## Summary

(Jim Manico) a read-only STRIDE threat model with file-and-line evidence.

## Content

**[Grim Prompter `/threat-model`](https://github.com/jmanico/grim-prompter)** (Jim Manico): a read-only STRIDE threat model with file-and-line evidence. It also maps MCP tools to the credentials behind them and can diff a branch against a baseline. Effort ~10 min. It's a new repo with one maintainer, so pin a commit.
```bash
git clone https://github.com/jmanico/grim-prompter.git ~/grim-prompter
mkdir -p ~/.claude/skills && ln -s ~/grim-prompter/skills/threat-model ~/.claude/skills/threat-model
# /threat-model   or   /threat-model change main...feature
```

## Sources

- [grim-prompter](https://github.com/jmanico/grim-prompter)
