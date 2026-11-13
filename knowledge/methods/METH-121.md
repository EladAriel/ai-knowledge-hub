# METH-121: Lightfoot: GraphRAG where deleting a document needs no LLM

## Summary

Every entity and link in the graph comes only from what was extracted from individual passages, and each one points to its source chunk. Deleting a document is then a plain database operation.

## Details

Results: after deleting 10% of documents, the graph was identical to a full rebuild; LightRAG needed 2,187 model calls and 3.7 hours for the same deletion. Indexing costs 26–31% less than HippoRAG 2, and it scores better on MuSiQue and HotpotQA. It is worse on 2WikiMultiHopQA (top-2 recall down 3.9 points), and the paper says so. Why it matters: when access is revoked or a deletion request comes in, the graph has to truly forget the data. Effort: medium. Adopt for: Architects make 'deletable without an LLM' a rule for every graph or memory store; Product track how long it takes to fully forget a document as a compliance metric; Devs add a test that deletes N documents, rebuilds from the rest, and checks the two graphs match. Code: udayallu-ml/Lightfoot-GraphRAG (see TOOL-044). arXiv 2611.11010.

## Sources

- [Lightfoot (arXiv)](https://arxiv.org/abs/2611.11010)
- [Lightfoot-GraphRAG](https://github.com/udayallu-ml/Lightfoot-GraphRAG)
