# PIPE-013: Pipeline: retrieval + calibrated reranking

## Summary

query -> optional rewrite -> permission-filtered BM25 + vector (top 50-100 each) -> RRF -> cross-encoder rerank -> keep ….

## Details

Choose candidate depth by measured candidate recall on the golden set. Don't threshold merged scores (RRF tops out at 2/61 with two retrievers; min-max makes the best weak match 1.0). ….

## Sources

- [AWS hybrid search write-up](https://builder.aws.com/content/3KJyvPGmUnCxmFR0gG2wGkHoYTR/hybrid-search-and-reranking-what-each-one-actually-buys-you)
