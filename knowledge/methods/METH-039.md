# METH-039: Chunker decides your re-embedding bill (boundary drift)

## Summary

After edits, chunk boundaries shift: fixed-size chunking re-did 57-68% of embedding work, recursive 38-56%, content-defined 43-54%; recall within 2 points.

## Details

Static evals see the chunkers as equal while update costs differ. Short paper, Wikipedia only. Key embeddings by a hash of chunk text, not position: add chunk_sha256, skip embed if hash exists, log reuse % per sync; track update cost next to recall.

## Content

### 1. Chunk Recomputation under Real Document Revisions: the chunker decides your re-embedding bill
- URL: https://arxiv.org/abs/2610.31019 (submitted 2026-10-22, accepted at AIBDCC 2026)
- What: when a document is edited, chunk boundaries can shift ("boundary drift"), so text that did not change still gets re-embedded. Test set: 120 pairs of back-to-back Wikipedia revisions (EN + ZH), byte-identical reuse rule, frozen encoder.
- Numbers (from the paper): fixed-size chunking recomputes **57-68%** of the new version's embedding work, recursive **38-56%**, content-defined chunking **43-54%** (CDC failed on 4 of 62 Chinese articles). Evidence recall at a 2048-token budget differed by **less than 2 points**. So static evals see these chunkers as equal, but their update cost is very different.
- Why it matters: a Company Brain re-ingests Confluence, Docs and tickets all the time. Fixed-size chunking was the most expensive to update in every length-matched setting. Limits: short paper, Wikipedia only, stateless chunkers only.
- Adopt for:
  - Architects: key embeddings by content hash, not by (doc_id, chunk_index). Track "update cost" next to recall when you choose a chunker.
  - Product: frequent edits mean cost and latency. Give a re-index cost estimate per source, for example a busy wiki compared with static PDFs.
  - Devs: add a `chunk_sha256` column, skip the embed call when the hash already exists, and report the % reused per sync job.

## Sources

- [Chunk Recomputation under …](https://arxiv.org/abs/2610.31019)