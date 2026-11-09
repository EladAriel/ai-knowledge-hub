# DEVX-046: human-gate mod: irreversible actions wait for a human (auto mode can't approve)

## Summary

claude-code-templates security mod: deploys, publishes, pushes to protected branches, payments, outbound messages, destructive SQL and MCP write tools require a person; auto mode and allow rules can't skip it; refused in claude -p; fails closed.

## Details

Since 2.1.304 a mod's 'ask' belongs to a person. Categories: deploy (terraform apply, kubectl apply, vercel --prod, gh workflow run...), publish (npm/pnpm/cargo/twine/docker push/gh release), push-main, money (Stripe MCP write tools, refunds, payouts, invoices), outbound (MCP send/post/reply/share/comment), data (DROP/TRUNCATE/ALTER, DELETE/UPDATE without WHERE, prisma/alembic/rails migrations). Splits compound commands, skips quoted text, lets --dry-run through; read-only calls get a no-prompt fast lane (MCP only if trustMcpReadOnly). Differs from agentfence (Nov 2): in-engine, auto mode can't override, covers MCP tools. Heuristic, not a sandbox (sh -c with a variable command isn't seen). Merged Nov 3 in PR #1366; untested.

## Sources

- [human-gate mod (claude-code-templates)](https://github.com/davila7/claude-code-templates/tree/main/cli-tool/components/mods/security/human-gate)
