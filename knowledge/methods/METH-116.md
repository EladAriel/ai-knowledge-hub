# METH-116: Aegis OS: transaction-level permission instead of per-action approval

## Summary

Each coding agent runs in a copy-on-write shadow workspace inside a kernel sandbox. An egress proxy injects secrets as placeholders. Human approval is required only at workspace commit via three-way merge.

## Details

What's new: the permission boundary moves from a single tool call to a transaction boundary, to fight approval fatigue. Evidence (author-reported): 90.7%–97.9% fewer approvals in 52 real sessions; attack success 100%→0% on 80 attacks with per-component ablation. Limits: single author, one star, paid cloud behind the project; all numbers self-reported. Scores: effectiveness 3/5, hype 3/5. Fit: free-run-in-sandbox + one gate at commit suits any action-taking agent product. Effort: medium. Recommendation: Pilot the pattern, not the product. Code: heurion-org/aegis-os. arXiv 2611.08516.

## Sources

- [Aegis OS (arXiv)](https://arxiv.org/abs/2611.08516)
- [aegis-os](https://github.com/heurion-org/aegis-os)
