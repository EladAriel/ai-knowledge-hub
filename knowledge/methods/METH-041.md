# METH-041: The fusion tax: hybrid retrieval hurts many individual queries

## Summary

Even the best BM25+dense fusion ranked relevant docs below the better single retriever on 13-48% of queries, while ….

## Details

7 BEIR datasets, 5 dense encoders, SPLADE, 3 fusion functions; RRF pays more when dense is clearly stronger; exact IDs/codes fail most. Make fusion a per-source setting; log both rankers' rank for the gold chunk; ….

## Sources

- [The Fusion Tax](https://arxiv.org/abs/2610.30612)
