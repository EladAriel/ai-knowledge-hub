# DEVX-053: pre-mortem skill (claude-code-templates): assume the plan failed, rank causes, set tripwires

## Summary

Before a launch, migration or architecture change, Claude assumes the plan already failed, lists failure stories, ranks them by likelihood, impact and early warning, assigns prevent/detect/respond mitigations with owners, and ends with tripwires and a go/no-go call.

## Details

Part of a 'thinking skills' pack (five-whys, tradeoff-analysis, thinking-method-selector); has a light path for small asks (6 causes, top 3). MIT, author ysskrishna, merged Nov 3 in PR #1201; untested. Install: npx claude-code-templates@latest --skill productivity/pre-mortem --yes. SKILL.md steps: 1. Imagine (one past-tense sentence: 'It is [date]. The [plan] failed badly: [failure definition].') ...

## Sources

- [pre-mortem skill](https://github.com/davila7/claude-code-templates/tree/main/cli-tool/components/skills/productivity/pre-mortem)
