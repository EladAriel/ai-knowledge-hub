# METH-018: Usefulness score + threshold instead of embedding top-k (GPT Researcher)

## Summary

Keep a chunk only if a usefulness score clears a threshold; 73% of kept passages relevant vs 46% with embeddings.

## Content

### 3. [GPT Researcher replaced embedding similarity with a "usefulness" score plus a threshold](https://docs.gptr.dev/docs/gpt-researcher/gptr/context-filter) (late Sep) | Effort: **low**
- **What:** each chunk gets a usefulness score from Jev (TypeSafe's scoring model), and only chunks at or above `JEV_MIN_SCORE=1.5` are kept. On 28 tasks, 73% of kept passages were relevant vs 46% with embeddings. Reports won 15–3 in head-to-head comparisons, at about the same cost per report (~$0.115). The fallback with no API key is BM25 keyword ranking, which also beat embeddings at 51% ([release notes](https://github.com/assafelovic/gpt-researcher/discussions/2174)).
- **Key lesson:** the threshold matters more than the ranking. Forced to fill all 10 slots, precision fell from 73% to 50%.
- **Limitations:** this is the team's own benchmark. An [independent benchmark](https://github.com/emretheus/jev-rag-benchmark) found Jev statistically tied with, or slightly behind, a dedicated cross-encoder reranker. Jev is a paid API.
- **Adopt for:**
  - *Architects:* treat context selection as its own stage with a "keep or drop" decision, not just top-k.
  - *Product:* measure the share of kept context that is relevant, plus context tokens per answer (cost).
  - *Devs:* add a calibrated score threshold to your current reranker, with a BM25 baseline, and compare on your golden set before buying anything.

## Sources

- [GPT Researcher replaced embedding similarity with a "usefulness" score plus a threshold](https://docs.gptr.dev/docs/gpt-researcher/gptr/context-filter)
- [release notes](https://github.com/assafelovic/gpt-researcher/discussions/2174)
- [independent benchmark](https://github.com/emretheus/jev-rag-benchmark)
