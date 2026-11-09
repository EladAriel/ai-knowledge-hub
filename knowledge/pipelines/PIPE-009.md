# PIPE-009: Pipeline: parsing and chunking

## Summary

raw file -> route (text layer or vision parser) -> typed blocks with page, bbox, reading order -> structure-aware chunks -> add context -> hash and embed -> index with doc-identity metadata.

## Details

Carry a heading stack across pages and pack whole sentences (Akamai: fragments 43% -> 1%). Embed chunk with heading path and doc title. Contextual note per chunk (Anthropic Contextual Retrieval: -49% top-20 failures, -67% with reranker). Tables first-class: one per chunk with caption, split by rows, repeat header; store parser version. Choose boundaries with update cost in mind (hash cache, recursive over fixed). Chunk schema: doc_id, version, section path, page+bbox, block type, parser version, content hash.

## Content

## (C) Pipeline pattern of the day: parsing / chunking

**Flow:**
Raw file -> Route (born-digital text layer vs scan/complex page -> VLM parser) -> Typed blocks with provenance (heading/paragraph/table/figure + page + bbox, reading order) -> Structure-aware chunking (heading stack carried across pages, sentence packing, one table per chunk with repeated header) -> Contextualize (heading path + doc title/identity prefix; optional LLM situating note) -> Hash + embed (reuse on unchanged hash) -> Index with doc-identity metadata

**Enterprise practices (each with a source):**
1. **Keep a heading stack during the single parse pass and carry it across page boundaries. Split on sentences, not pages, with a guarded join.** Akamai measured 43% of stored claims as sentence fragments with page-based splitting, and 1% after the fix. Also: keep headings out of body text, and record cross-references ("section 67") in a field without resolving them at parse time. https://www.akamai.com/blog/ai/sentence-forgets-preserving-context-document-ingestion
2. **Embed the contextualized chunk, not the bare text.** Docling's `contextualize()` adds headings and captions. Use the embedding model's tokenizer for split/merge, and repeat table headers when a table spans chunks. https://docling-project.github.io/docling/concepts/chunking/
3. **Add a short chunk-situating context.** Anthropic's Contextual Retrieval cut top-20 retrieval failures by 49%, and by 67% with reranking (older 2024 post, still the reference). https://www.anthropic.com/engineering/contextual-retrieval
4. **Tables are first-class:** keep them as HTML/Markdown, one table per chunk with caption + nearest heading, split long tables by rows with the header repeated, and store the parser version so you can re-chunk without paying for OCR again. https://balazscsorba.com/blog/pdf-document-parsing-for-rag
5. **Choose chunk boundaries with update cost in mind:** content-hash chunk reuse, and prefer recursive/content-aware chunking over fixed-size for docs that change often. https://arxiv.org/abs/2610.31019 (late chunking is the alternative when you need document-wide context in each vector without generating text: https://arxiv.org/abs/2409.04701)

**Who owns what:**
- Architects
  - Own the **chunk schema contract**: doc_id, version, section path, page + bbox, block type, parser + chunker version, content hash, references list. Every parser must produce it.
  - Own the routing policy (text-layer vs VLM) and the re-parse/re-chunk strategy, with the raw parse stored as the source of truth.
- Product
  - Pick the 30-50 "money pages" (tables, scans, forms, slides) that represent real user questions, and make them the parser/chunker acceptance set.
  - Decide where citations must point to a page region (needs bbox) and where doc-level citations are enough.
- Devs
  - Use Docling HybridChunker (or chonkie for A/B) with `contextualize()` for embedding text. Add the heading stack across pages, sentence packing, and table header repeat.
  - Add a chunk-hash embedding cache, plus CI checks for fragment rate and the span-containment test (D).

---

## Sources

- [Akamai](https://www.akamai.com/blog/ai/sentence-forgets-preserving-context-document-ingestion)
- [Anthropic Contextual …](https://www.anthropic.com/engineering/contextual-retrieval)
- [Docling chunking](https://docling-project.github.io/docling/concepts/chunking/)