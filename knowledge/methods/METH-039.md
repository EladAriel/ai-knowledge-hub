# METH-039: Chunker decides your re-embedding bill (boundary drift)

## Summary

After edits, chunk boundaries shift: fixed-size chunking re-did 57-68% of embedding work, recursive 38-56%, ….

## Details

Static evals see the chunkers as equal while update costs differ. Short paper, Wikipedia only. Key embeddings by a hash of chunk text, not position: add chunk_sha256, skip embed if hash exists, log reuse % per sync; ….

## Sources

- [Chunk Recomputation under …](https://arxiv.org/abs/2610.31019)
