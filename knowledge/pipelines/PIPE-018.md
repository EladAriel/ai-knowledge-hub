# PIPE-018: Pipeline: parsing and chunking (heading-aware)

## Summary

raw file -> parse with layout, reading order and element positions -> check a sample against original pages -> split at headings -> group paragraphs into chunks per section -> prepend heading path -> index with page and position.

## Details

Split at headings first: in a measured test on the FastAPI docs, BM25 top-1 hit rose 0.39 -> 0.71 with heading splits and 0.79 with heading path; over half of fixed-size chunks crossed two sections (caveat: queries were the headings themselves). Keep tables whole with headers (HTML spanning cells, as DPP). Keep page number and position of every element/chunk for exact citations (Parsy). Check parse quality on a sample via reconstruction; send low scorers to review. Keep the raw file so you can re-parse. Owners: Architects own the parsing contract (DPP version, keep-raw rule); Product owns the review queue and doc-type priority; Devs own the chunker, heading path, and a small CI check of right-chunk-in-top-results.

## Sources

- [heading-aware chunks test](https://dev.to/recallrundev/rag-chunking-measured-heading-aware-chunks-doubled-hit1-on-the-fastapi-docs-5hh7)
