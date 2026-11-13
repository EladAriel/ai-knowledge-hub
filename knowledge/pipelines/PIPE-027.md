# PIPE-027: Pipeline: parsing and chunking (layout, structure, searchable coverage)

## Summary

file -> parser chosen by format, keeping layout, reading order and page positions -> remove headers, footers and hidden injected text -> chunk by structure (a section, a slide, or a table row with its header) -> check token limits -> embed with context, like the heading at the front -> count how many chunks per document are searchable.

## Details

Chunk the way a person sees the document: a section under its heading, one slide with its notes, or a table row with its header row. Store the document, page and heading with every chunk so citations work (Tecifo). Measure characters per token on your own content—tables of dates and amounts came out at 1.65 characters per token vs about 4 for normal text; character limits break on tables. Never let one rejected chunk silently stop the rest; log rejected chunks and track the share of chunks that are searchable. Score parsing separately from answers (Parse and Hold). If you use late chunking, the hardest wrong result is a neighbouring chunk from the same document (arXiv 2611.12097; treat as optional). Owners: Architects own the chunk format as a data contract (source ID, page, headings, version, permissions); Product picks the 3 document types that matter most and sets a target, for example 99.5% of chunks searchable; Devs hide the parser and chunker behind one interface with a config setting, so parsers are easy to swap and compare.

## Sources

- [Tecifo ingestion](https://tecifo.com/insights/rag-pdf-docx-pptx-ingestion)
- [RAG on tax PDFs](https://polischuks.dev/blog/rag-on-tax-pdfs/)
- [Parse and Hold](https://parseandhold.com/posts/tracing-rag-hallucinations-upstream-to-malformed-extraction-output)
- [late-chunking sibling paper](https://arxiv.org/abs/2611.12097)
