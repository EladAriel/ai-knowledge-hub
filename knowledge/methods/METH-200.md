# METH-200: Amazon S3 Vectors adds hybrid search

## Summary

Embeddings miss exact terms like part numbers, ticket IDs and spec codes. S3 Vectors now runs keyword search and vector search together in one query, then merges the results. Frequent queries take around 100 ms, at S3 storage prices. Why it matters: if your stack is already on AWS, this is a cheap hybrid store with no extra search cluster. It is a release note only, with no quality numbers. Next step: turn on full-text search for one text field you already store, and test 20 exact-code queries. For: architects.

## Details

Reported Nov 23. Complements today's identifier lookup test (EVAL-046) and the indexing practice in PIPE-038.

## Sources

- [Amazon S3 Vectors hybrid search](https://aws.amazon.com/about-aws/whats-new/2026/11/s3-vectors-hybrid-search/)
