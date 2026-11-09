# PIPE-009: Pipeline: parsing and chunking

## Summary

raw file -> route (text layer or vision parser) -> typed blocks with page, bbox, reading order -> structure-aware ….

## Details

Carry a heading stack across pages and pack whole sentences (Akamai: fragments 43% -> 1%). Embed chunk with heading path and doc title. Contextual note per chunk (Anthropic Contextual Retrieval: -49% top-20 failures, -67% with ….

## Sources

- [Akamai](https://www.akamai.com/blog/ai/sentence-forgets-preserving-context-document-ingestion)
- [Anthropic Contextual …](https://www.anthropic.com/engineering/contextual-retrieval)
- [Docling chunking](https://docling-project.github.io/docling/concepts/chunking/)
