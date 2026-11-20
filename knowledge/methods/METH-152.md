# METH-152: AsteroRank: give the reranker the agent's goal

## Summary

The agent sends the reranker a short keyword query plus a few sentences on what it already knows and what it's looking for. Filters stay with the agent and run after the first search. Vendor blog, Nov 6. Benchmarks are the vendor's own.

## Details

They report this improved ranking quality far more than rewording the query did. There is a 4B open model (AsteroRank-Lepton) whose license allows no commercial use. The stronger models are behind a (the source note was cut off after this phrase). This matches the Nov 13 permissions theme: rerankers judge relevance, not permissions, and filters stay in the engine.

## Sources

- [AsteroRank blog](https://blog.asteromorph.com/asterorank/)
- [AsteroRank-Lepton](https://huggingface.co/Asteromorph/AsteroRank-Lepton)
