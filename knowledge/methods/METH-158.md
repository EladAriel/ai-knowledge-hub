# METH-158: New terms (Nov 15, enterprise knowledge): proactive agent, correct silence, timeout counted as silence, parametric claim, AURC, verify before declining, goal engineering

## Summary

One-line terms (Nov 15) on the answer layer.

## Details

Proactive agent: watches work channels and decides on its own whether to speak. Correct silence: staying quiet when the issue is already handled. Timeout counted as silence: a scoring bug where a run that ran out of time gets credit for choosing to stay quiet. Parametric claim: a cited claim that really came from the model's memory. Value-swap test: change a value in the sources and ask again; if the answer stays the same, it came from memory. Risk-coverage curve: shows accuracy against the share of questions answered as the confidence cutoff moves; AURC is the area under it (lower is better). Warning-induced over-refusal: refusing normal work because of a planted fake warning. Verify before declining: refuse only when an official record confirms the risk. Patch, never regenerate: after the first draft, only targeted edits, so checked parts don't quietly change. Goal engineering: scoping an agent to one repeatable job type so human feedback is easy to give and reuse. Recurring themes: declining is now a proper outcome, and today that extends to staying quiet — restraint can also be attacked; enforce rules in code, not prompts, now including the decline threshold; citation honesty, last seen Nov 4, now has a measured rate; cost per correct answer, from Nov 8, shows up again in Deepnote's cost-versus-score chart.

## Sources

- No single link was recorded for this terms list. Related public sources (see PIPE-032, METH-154 to METH-157):
- [Deepnote Agent Initiative Benchmark](https://deepnote.com/research/benchmark)
- [Abstention threshold paper](https://arxiv.org/abs/2611.14661)
- [Fake-warning over-abstention](https://arxiv.org/abs/2611.14864)
- [Cited but Unused](https://arxiv.org/abs/2611.17161)
- [LangChain: goal engineering](https://www.langchain.com/blog/goal-engineering)
