# METH-185: ARISE: an agent that learns from its own mistakes, and keeps a rule only if held-out accuracy rises (Pilot)

## Summary

When the agent fails, a model finds the cause and saves a small fix to memory. Small fixes get merged into general rules. A new rule is kept only if accuracy on test questions the agent hasn't seen goes up. The authors report +10.9 points on SOP-Bench (14 domains, 5 models) and +5.8 on τ²-bench, at about the same cost, and say it beats GEPA. Even without an external teacher model, they report a 10-point gain. No code was found. Recommendation: Pilot. Effort: medium. arXiv 2611.23588.

## Details

Noted on Nov 19.

Why it matters: it is the same loop as yesterday's gap mining (PIPE-033 / METH-172), except the agent fixes itself, with a safety check before a new rule goes live. The idea of an acceptance gate on memory already appeared here (Gated Memory / FGSE, METH-127). What is new is results on organizational procedures.

Limits: author-reported numbers, and no code. Next step: copy the check. A new rule or memory goes live only if your set of test questions with known answers scores better. For: devs and architects.

## Sources

- [ARISE](https://arxiv.org/abs/2611.23588)
