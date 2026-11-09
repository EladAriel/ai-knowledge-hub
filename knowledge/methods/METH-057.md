# METH-057: Calibrated reranker thresholds (Cohere Rerank 5) and their scale problem

## Summary

Calibrated scores let you keep docs above a threshold (or say 'no evidence'); but fixed relevance cutoffs degrade as the store grows.

## Details

Cohere Rerank 5: score ~ probability a doc is useful; Context Focus returns best passages (half the context -2 pts, three-quarters -7 pts; Cohere's numbers, own RCP-nDCG metric). Price of Scale paper: a threshold tuned for 5% false alarms on 8 items gave 87-100% on 2,048; LLM judges degrade too; raise threshold with store size or use a cue-swap check. Version threshold with model; put reranker behind an interface; 'no evidence found' is a real contract result.

## Content

**1. [Cohere Rerank 5](https://cohere.com/blog/rerank-5)** (Oct 21)
- Its scores are calibrated, meaning each score is roughly the probability that a doc is useful. So you keep everything above one threshold instead of always passing a fixed top-k. If nothing passes, the agent knows to rewrite the query or say it doesn't know.
- A feature called "Context Focus" returns the best passages inside each doc. Cohere says cutting half the context cost 2 points of answer quality, and cutting three-quarters cost 7 points.
- Caveat: these are Cohere's own numbers, and the ranking claim uses a metric Cohere defined (RCP-nDCG), so check it on your own data.
- Adopt for:
  - *Architects:* version the threshold together with the model, and make "no evidence found" a real result in the contract.
  - *Product:* track how often nothing relevant is found. Each of those is missing content you can add.
  - *Devs:* put the reranker behind an interface, so config can switch between Cohere, a self-hosted model, or no reranker.

**2. [The Price of Scale in Proactive Memory Recall](https://arxiv.org/abs/2610.34507)** ([code](https://github.com/RiverChenStillCompiling/price-of-scale))
- A similarity threshold tuned for 5% false alarms on a store of 8 items gave 87–100% false alarms on 2,048 items. LLM judges got worse in the same way.
- Why it matters: any fixed "is this relevant?" cutoff gets worse as the store grows. The fixes are to raise the threshold as the store grows, or to use the authors' "cue-swap" check, wh...on, not the paper's.

Also worth knowing: [Memory Tax](https://arxiv.org/abs/2610.34073) found that many dedicated agent-memory systems do worse than plain RAG. That's the "measure against a simple baseline" theme again.

## Sources

- [Cohere Rerank 5](https://cohere.com/blog/rerank-5)
- [The Price of Scale in Proactive Memory Recall](https://arxiv.org/abs/2610.34507)
- [code](https://github.com/RiverChenStillCompiling/price-of-scale)
- [Memory Tax](https://arxiv.org/abs/2610.34073)