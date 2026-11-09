# DEVX-057: five-whys skill (claude-code-templates): evidence-backed root-cause analysis with countermeasures

## Summary

Root-cause skill following the Toyota 5 Whys: state the problem, ask why with verified/hypothesis evidence at each step, stop at a cause the team can change, then set countermeasures. Sibling of the pre-mortem skill from the same thinking-skills pack.

## Details

MIT, author ysskrishna, merged Nov 3 in PR #1201 together with pre-mortem and tradeoff-analysis. Skip it for typos or already-proven causes. Not tested by the DevEx agent. Install: npx claude-code-templates@latest --skill productivity/five-whys --yes. Related: pre-mortem skill row (Nov 4).

## Content

**[five-whys skill (claude-code-templates productivity; sibling of yesterday's pre-mortem from the same thinking-skills pack)](https://github.com/davila7/claude-code-templates/tree/main/cli-tool/components/skills/productivity/five-whys)**
- **what_it_gives:** Root-cause skill from the Toyota Production System pattern: state the problem, ask why with verified/hypothesis evidence at each step, stop at a cause the team can change, then set countermeasures. Skip for typos or already-proven causes. MIT, author ysskrishna, merged Nov 3 in PR #1201 with pre-mortem (reported yesterday) and tradeoff-analysis. Not tested here.
- **effort_minutes:** 5
- **snippet:** npx claude-code-templates@latest --skill productivity/five-whys --yes

# SKILL.md frontmatter, verbatim
---
name: five-whys
description: >
  Use for the 5 Whys, or when the user wants the root cause of a failure: "why did this happen?", "this keeps breaking", "write the postmortem", "find the real cause". Asks why repeatedly with evidence at each step, then sets countermeasures. Skip for one-off typos or when the cause is already proven.
license: MIT
---
- **source_credit:** davila7/claude-code-templates cli-tool/components/skills/productivity/five-whys/SKILL.md (author ysskrishna), PR #1201

## Sources

- [five-whys skill](https://github.com/davila7/claude-code-templates/tree/main/cli-tool/components/skills/productivity/five-whys)