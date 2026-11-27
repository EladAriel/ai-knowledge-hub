# METH-214: One test run hides an unreliable agent

## Summary

Agentic RAG is usually scored on a single run, but the agent makes different search choices each time. The team ran 739 real product-docs questions 10 times each on a deployed system. The right page was found in at least one run 69.4% of the time, but in every run only 50.9% of the time. Retrieval caused 43.9% of the differences between runs, and the number of parallel searches at step one alone caused 20.1%. Why it matters: a demo that "works" can still fail for a fair share of users. You can make the first search step more fixed to cut that variation. Limits: one system, one domain, no code. Next step: fix the number of first-step searches, or make it rule-based, and re-measure. For: product and devs. arXiv 2611.31266.

## Details

Reported Nov 25. Related: EVAL-024 (pass^k, repeat-run consistency).

## Sources

- [One test run hides an unreliable agent](https://arxiv.org/abs/2611.31266)
