# METH-041: The fusion tax: hybrid retrieval hurts many individual queries

## Summary

Even the best BM25+dense fusion ranked relevant docs below the better single retriever on 13-48% of queries, while winning on average.

## Details

7 BEIR datasets, 5 dense encoders, SPLADE, 3 fusion functions; RRF pays more when dense is clearly stronger; exact IDs/codes fail most. Make fusion a per-source setting; log both rankers' rank for the gold chunk; alert when fusion \< max(single) share rises; track 'queries made worse'.

## Content

### 4. The Fusion Tax: hybrid BM25 + dense retrieval hurts many individual queries
- URL: https://arxiv.org/abs/2610.30612 (2026-10-22)
- What: across 7 BEIR datasets, 5 dense encoders (22M-596M), SPLADE and 3 fusion functions, even the best fusion (dense-weighted score interpolation) ranked relevant docs below the better single retriever on **13-48%** of queries, and below dense-only on **8-21%**. It still won in aggregate. RRF pays the higher tax when dense is clearly stronger.
- Why it matters: "always use hybrid + RRF" is the default advice. The paper says the fusion decision should depend on the measured sparse-dense balance of your corpus. It also links to chunking: queries that only one retriever covers (exact IDs, codes) are where fusion fails.
- Adopt for:
  - Architects: make fusion a per-source setting (code/tickets vs prose wiki), not one global constant.
  - Product: aggregate gains can hide per-query regressions that users see. Track "queries made worse" as well as the average.
  - Devs: log both rankers' ranks for the gold chunk. Count queries where fusion < max(single) and alert when the share rises.

---

## Sources

- [The Fusion Tax](https://arxiv.org/abs/2610.30612)