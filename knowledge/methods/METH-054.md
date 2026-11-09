# METH-054: No single least-privilege set for agent tool authorization

## Summary

For 29.8-33.3% of Microsoft Graph tasks two minimal permission sets each allow something the other doesn't.

## Content

**2. [Incomparable Minima in Agent Tool Authorization](https://arxiv.org/abs/2610.31914)** (arXiv, Oct 26)
- **The finding:** the authors analyzed 22,305 Microsoft Graph and 23,852 Google API permissions. For 29.8–33.3% of Graph tasks there's no single "smallest" set of permissions: two minimal sets each allow something the other doesn't.
- **How models did:** six frontier models picked a minimal set 99% of the time, but only 66.7% picked the one that was smallest on all four risk measures.
- **Limit:** it only analyzes the published permission lists, not live systems.
- Adopt for:
  - *Architects:* don't treat "least privilege" for agents as ...tps://github.com/authzed/workshops/tree/main/secure-rag-pipelines) shows it in a LangGraph and Qdrant RAG pipeline.
- What to borrow: `prefilter_node.py`, which asks SpiceDB for the doc IDs the user can view and passes them to Qdrant as the search filter.
  - The workshop also shows why filtering after search fails. A contractor can see 7 of 50 docs, so a top-5 search filtered afterwards often comes back empty.
  - It has a placeholder where `allowed_doc_ids: None` means "no restriction." That's exactly the fail-open bug you want to test for.
- Maturity: SpiceDB has 7.2k stars, Apache-2.0, pushed Oct 22, and runs with `docker run authzed/spicedb serve`. The workshop is young and has no license file.
- Best for: Architects and Devs.

## Sources

- [Incomparable Minima in Agent Tool Authorization](https://arxiv.org/abs/2610.31914)
