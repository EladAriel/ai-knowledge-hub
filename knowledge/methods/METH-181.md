# METH-181: Lightfoot: GraphRAG that deletes documents exactly, with no model calls (Pilot)

## Summary

Every entity, relation and fact in the graph is derived deterministically from each chunk's extraction, with a record of the source, and retrieval runs without an LLM. Deleting a document is a database transaction: deleting 10% of a corpus of 11,402 chunks took 14 seconds, and afterwards the graph was identical to re-indexing what remained. Recommendation: Pilot. Effort: medium. arXiv 2611.11010; code: udayallu-ml/Lightfoot-GraphRAG. Single author, at Yellow.ai.

## Details

What is new: most GraphRAG work ignores deletion, even though it is a real enterprise requirement because of GDPR and permissions. In HippoRAG 2, for example, after a deletion 565 relations remain that do not match a rebuild.

Evidence: there is code, and a comparison to HippoRAG 2 on MuSiQue, 2Wiki and HotpotQA with statistical tests. The results are competitive, but not superior. Effectiveness 3/5, hype 1/5. Fit is high for company-brain and enterprise-knowledge systems.

## Sources

- [Lightfoot GraphRAG](https://arxiv.org/abs/2611.11010)
- [udayallu-ml/Lightfoot-GraphRAG](https://github.com/udayallu-ml/Lightfoot-GraphRAG)
