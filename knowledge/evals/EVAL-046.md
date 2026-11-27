# EVAL-046: Eval: identifier lookup test

## Summary

A half-day eval (Nov 23). Write 30 questions that hinge on an exact token, such as a part number, error code or ticket ID. Measure how often the right document is in the top 5, once with vector search only and once with hybrid search. If vector-only scores under about 80%, hybrid is a must-have, not an extra.

## Details

What it catches: embeddings that miss exact terms like part numbers, ticket IDs and spec codes, even when the document is in the index.

Who runs it: Devs run the two searches and record hit@5. Architects decide whether hybrid is required. Product supplies the 30 exact-token questions from real work.

Complements the indexing practice in PIPE-038 and the S3 Vectors item (METH-200).

Effort: half a day.

## Sources

- [Amazon S3 Vectors hybrid search (METH-200)](https://aws.amazon.com/about-aws/whats-new/2026/11/s3-vectors-hybrid-search/)
- [PIPE-038: filter during the search, and keep a raw-text field](../pipelines/PIPE-038.md)
