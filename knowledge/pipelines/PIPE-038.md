# PIPE-038: Pipeline: indexing — filter during the search, and keep a raw-text field

## Summary

Indexing angle (Nov 23): keep permissions, source and date as fields inside the search index, and filter during the search, not after you already took the top results. That later cut silently drops allowed documents. Also keep a raw-text field next to the vector, for exact lookups.

## Details

This differs from earlier indexing angles (PIPE-011, PIPE-020, PIPE-029). PIPE-029 already said to apply filters inside the query and to keep raw text for keyword search. Today's practice is the reason that later cut is harmful (it silently drops documents the user is allowed to see) and the exact-lookup field that sits next to the vector.

Who owns it: Architects put permission, source and date fields in the index and require the filter to run during the search. Devs keep a raw-text field next to every vector. Product checks that permission-filtered questions still return the documents the user is allowed to see.

See also TOOL-019 (ParadeDB, one index for text, filters and vectors), METH-200 (S3 Vectors hybrid search), and EVAL-046 (identifier lookup test).

## Sources

- [ParadeDB: text, filters, and vectors in one Postgres index (TOOL-019)](https://www.paradedb.com/blog/filter-aware-vector-search)
- [Amazon S3 Vectors hybrid search (METH-200)](https://aws.amazon.com/about-aws/whats-new/2026/11/s3-vectors-hybrid-search/)
