# METH-175: StaleBench: stale retrieval in agent memory, and what the fix costs

## Summary

892 real facts that change over time (Wikidata validity years via TempLAMA). For "what is X now?" questions, similarity retrieval returns a stale version 53–59% of the time when it stores every version (repo README). Effort: low to measure, medium to fix. arXiv 2611.19752, Nov 15; code: thenexuslab/stalebench-release.

## Details

Key finding: retrieval metrics can rank memory policies backwards. Two policies return the same statement at rank 1 for every query, yet differ by 29.5 and 65.6 points in reader accuracy. The new metric contamination@5 ranks them correctly. Time-reranking lifts current@1 from 0.464 to 0.925 but leaves stale versions in the context (contam@5 still 0.974).

Deployed systems: Mem0, Graphiti and LangMem each handle supersession differently. For example, Graphiti's contam@5 is 0.947 as returned and 0.120 with valid edges first (150-fact subsample). Limits: encyclopedic facts, not enterprise documents. Entity resolution on both the write path and the query recovers most of the keying loss.

Adopt for: Architects treat valid-from/valid-to plus an entity key at write time as a requirement for memory. Product adds a freshness metric for current-value questions to the dashboard. Devs track contamination@5 next to recall@k, because top-1 can hide stale context. See also TOOL-050.

## Sources

- [StaleBench](https://arxiv.org/abs/2611.19752)
- [stalebench-release](https://github.com/thenexuslab/stalebench-release)
