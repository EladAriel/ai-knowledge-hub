# METH-213: Rerank once per search step, not over and over

## Summary

Search agents run many searches for one question. Adding a reranker at every step makes them slower and more expensive, and it often ranks results only against the agent's sub-question, so the original question gets lost. The fix is one fast scoring model, with no training needed, that picks the relevant passages from long docs and reranks them in a single call. It scores against both the original question and the sub-question. On a public web benchmark, a small model went from 73.9% to 84.7% accuracy, and searches dropped from 23 to 14. Why it matters: if your company brain lets an agent loop over search, better reranking cuts the number of steps, so you save on cost as well as gaining quality. No code was published, and the numbers come from public web benchmarks, not company data. Next step: in your agent's search tool, pass the user's original question into the reranker along with the sub-question. For: devs and architects. arXiv 2611.32917.

## Details

Reported Nov 25. Complements today's retrieval practice in PIPE-040 and the depth sweep in EVAL-048.

## Sources

- [Rerank once per search step](https://arxiv.org/abs/2611.32917)
