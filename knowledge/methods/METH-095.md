# METH-095: When Do Summaries Become Instructions?: fabricated policy in handoff/compaction summaries

## Summary

Measures whether long-horizon agent compaction summaries invent permissions or limits that are not in the record, and whether the inheriting agent acts on them. Checked against a real permission ledger with replay from the same snapshot. First time compaction is measured as a source of forged policy, not only of information loss.

## Details

Evidence: unfounded approvals in 0.1%–1.3% of summaries; neutralizing them cut unauthorized actions from 24 to 7 of 120 runs (post-hoc); later set only 17→11 of 48. Strong pre-registered finding: rephrasing the system-prompt line 'Some actions need approval' cut invented limits from 1.8% to 0.3% (p \< 10⁻⁹). Effect on the limits themselves is fragile; author reports this openly. Scores: effectiveness 3/5, hype 1/5. Fit: any agent with compaction or handoff; add an eval that compares the summary to the permission ledger. Effort: low.

## Sources

- [When Do Summaries Become Instructions? (arXiv)](https://arxiv.org/abs/2611.06545)
- [handoff-audit](https://github.com/Chuw1/handoff-audit)
