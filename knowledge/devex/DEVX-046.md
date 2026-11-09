# DEVX-046: human-gate mod: irreversible actions wait for a human (auto mode can't approve)

## Summary

claude-code-templates security mod: deploys, publishes, pushes to protected branches, payments, outbound messages, destructive SQL and MCP write tools require a person; auto mode and allow rules can't skip it; refused in claude -p; fails closed.

## Content

**[human-gate (claude-code-templates, security): irreversible calls (deploy, publish, push to protected branch, Stripe and other payment calls, outbound messages, destructive SQL) wait for a human; auto mode and allow rules can't approve them; refused in `claude -p`](https://github.com/davila7/claude-code-templates/tree/main/cli-tool/components/mods/security/human-gate)**
- **what_it_gives:** Since 2.1.304 a mod's 'ask' belongs to a person, so the auto-mode classifier and allow rules can't approve it. Where nobody can be asked (headless `-p`), the call is refused with a reason. Categories: deploy (`terraform apply`, `kubectl apply`, `vercel --prod`, `gh workflow run`, ...), publish (npm/pnpm/cargo/twine/docker push/gh release), push-main, money (Stripe MCP write tools, refunds, payouts, invoices), outbound (MCP send/post/reply/share/comment tools) and data (DROP/TRUNCATE/ALTER, DELETE/UPDATE without WHERE, prisma/alembic/rails migrations). It splits compound commands, skips quoted text and lets `--dry-run` through. If the check throws, it fails closed (asks). Read-only tool calls get a no-prompt fast lane; MCP tools only if `trustMcpReadOnly`. How it differs from agentfence (reported Nov 2): it's an in-engine mod that auto mode can't override and that also covers MCP tools, not just shell text. It's a heuristic, not a sandbox (`sh -c "$CMD"` isn't seen). Merged Nov 3 in PR #1366. New and untested here.
- **effort_minutes:** 10
- **snippet:** npx claude-code-templates@latest --mod security/human-gate

# options live in ~/.claude/settings.json under
#   pluginConfigs["human-gate@skills-dir"].options
# categories        (default all)  deploy, publish, push-main, money, outbound, data
# protectedBranches (default)      main, master, production, prod, release
# extraCommands                    e.g. \bansible-playbook\b
# extraTools                       e.g. ^mcp__linear__save_issue$
# trustMcpReadOnly  (default false)
# then type /human-gate to see held / let-through counts
- **source_credit:** davila7/claude-code-templates, cli-tool/components/mods/security/human-gate/README.md (install line and Options table, condensed into comments), PR #1366

## Sources

- [human-gate mod (claude-code-templates)](https://github.com/davila7/claude-code-templates/tree/main/cli-tool/components/mods/security/human-gate)
