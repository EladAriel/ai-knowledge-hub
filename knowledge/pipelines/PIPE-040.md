# PIPE-040: Pipeline: retrieval and reranking — wide hybrid pool, rerank against the original question, send only the top passages

## Summary

Retrieval angle (Nov 25): pull a wide pool of 50–100 candidates with hybrid search, rerank it against the original question, and send only the top 5–8 passages, not document openings, to the model. Log reranker scores so you can later set a "not enough evidence" cutoff.

## Details

This differs from earlier retrieval angles (PIPE-004, PIPE-013, PIPE-022, PIPE-031), which were about phased ranking, a flexible budget, or giving the reranker the agent's goal. Today's practice is to keep the user's original question in the rerank, send short passages rather than document openings, and keep the scores so you can later refuse to answer when evidence is weak.

See also METH-213 (rerank once per search step, against both the original question and the sub-question) and EVAL-048 (rerank depth sweep).

## Sources

- [Rerank once per search step (METH-213)](https://arxiv.org/abs/2611.32917)
