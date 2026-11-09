# PIPE-018: Pipeline: parsing and chunking (heading-aware)

## Summary

raw file -> parse with layout, reading order and element positions -> check a sample against original pages -> split at headings -> group paragraphs into chunks per section -> prepend heading path -> index with page and position.

## Details

Split at headings first: in a measured test on the FastAPI docs, BM25 top-1 hit rose 0.39 -> 0.71 with heading splits and 0.79 with heading path; over half of fixed-size chunks crossed two sections (caveat: queries were the headings themselves). Keep tables whole with headers (HTML spanning cells, as DPP). Keep page number and position of every element/chunk for exact citations (Parsy). Check parse quality on a sample via reconstruction; send low scorers to review. Keep the raw file so you can re-parse. Owners: Architects own the parsing contract (DPP version, keep-raw rule); Product owns the review queue and doc-type priority; Devs own the chunker, heading path, and a small CI check of right-chunk-in-top-results.

## Content

## Pipeline pattern of the day: parsing and chunking

raw file -> parse with layout, reading order and element positions -> check a sample of parses against the original pages -> split at headings -> group paragraphs into chunks within each section -> add the heading path to each chunk -> index, keeping each chunk's page and position

- **Split at headings first.** In a [measured test on the FastAPI docs](https://dev.to/recallrundev/rag-chunking-measured-heading-aware-chunks-doubled-hit1-on-the-fastapi-docs-5hh7):
  - Splitting at headings raised how often keyword search (BM25) found the right chunk first, from 0.39 to 0.71.
  - Adding the heading path raised it to 0.79.
  - More than half of fixed-size chunks crossed two sections.
  - Caveat: the test queries were the headings themselves, so expect smaller gains with real questions.
- **Keep tables whole, with their headers.** Write multi-row headers as HTML with cells that span columns, as DPP does.
- **Keep the page number and position of every element and chunk,** so citations can point to the exact spot (Parsy).
- **Check parse quality on a sample** by rebuilding pages from the parsed output and comparing them to the originals. Send low scorers to review.
- **Keep the raw file,** so you can re-parse when your parser improves. This is the third time this month this advice has come up.
- **Who owns it:**
  - *Architects* own the parsing contract, meaning which DPP version you follow, and the rule to keep raw files.
  - *Product* owns the review queue and which document types to handle first.
  - *Devs* own the chunker, the heading path added to each chunk, and a small CI check of how often the right chunk is in the top results.

## Sources

- [heading-aware chunks test](https://dev.to/recallrundev/rag-chunking-measured-heading-aware-chunks-doubled-hit1-on-the-fastapi-docs-5hh7)