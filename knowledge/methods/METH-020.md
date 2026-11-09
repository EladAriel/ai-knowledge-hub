# METH-020: GraphRAG indexing cost reality check

## Summary

GraphRAG on one 41-page paper with a local 27B model: ~281 calls, ~2 h; another 26-page paper +73 min; ….

## Details

6 in 10 entities were people (bibliography chunks); the target relation was extracted once. HippoRAG failure analysis: 48% of errors from entity spotting, 28% from relation extraction. ….

## Sources

- [Sergii Makarevych on X](https://x.com/sermakarevich/status/2111515269638074660)
- [Neo4j tutorial](https://github.com/sermakarevich/tutorials/tree/main/graph_rag)
