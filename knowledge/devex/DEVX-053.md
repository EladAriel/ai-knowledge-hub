# DEVX-053: pre-mortem skill (claude-code-templates): assume the plan failed, rank causes, set tripwires

## Summary

Before a launch, migration or architecture change, Claude assumes the plan already failed, lists failure stories, ranks them by likelihood, impact and early warning, assigns prevent/detect/respond mitigations with owners, and ends with tripwires and a go/no-go call.

## Details

Part of a 'thinking skills' pack (five-whys, tradeoff-analysis, thinking-method-selector); has a light path for small asks (6 causes, top 3). MIT, author ysskrishna, merged Nov 3 in PR #1201; untested. Install: npx claude-code-templates@latest --skill productivity/pre-mortem --yes. SKILL.md steps: 1. Imagine (one past-tense sentence: 'It is [date]. The [plan] failed badly: [failure definition].') ... 3. Rank (| Cause | Likelihood | Impact | Early warning |) ... 5. Decide (tripwires; go/no-go: go as is, go with changes, or hold). Footnote: claude-code-templates 1.32.0 now reports in install telemetry whether an AI agent ran the install.

## Content

**[pre-mortem skill](https://github.com/davila7/claude-code-templates/tree/main/cli-tool/components/skills/productivity/pre-mortem)** assumes your plan, launch or migration has already failed. It then ranks the likely causes by likelihood, impact and early warning, and ends with tripwires and a go or no-go call. MIT license, by ysskrishna in claude-code-templates. Effort: ~5 min.
```bash
npx claude-code-templates@latest --skill productivity/pre-mortem --yes
```

Footnote: claude-code-templates 1.32.0 now records in its install telemetry whether an AI agent ran the install, so check that if your org uses its CLI.

## Sources

- [pre-mortem skill](https://github.com/davila7/claude-code-templates/tree/main/cli-tool/components/skills/productivity/pre-mortem)