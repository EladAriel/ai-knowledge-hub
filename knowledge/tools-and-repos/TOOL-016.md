# TOOL-016: Repos: Docling, Chonkie, Knowhere

## Summary

Document conversion with page/bbox; lightweight chunking library; dual-path parsing with navigable memory.

## Details

docling-project/docling (~69k, MIT, LF AI & Data): HybridChunker sized by embedding tokenizer, contextualize() for heading-prefixed text, repeat_table_header=True. feyninc/chonkie (~4.8k, MIT): Pipeline API to compare chunkers in minutes. Ontos-AI/knowhere (~3.7k, Apache-2.0, 6 months old, telemetry on by default): vision and text paths feed one chunk schema; design reference only.

## Content

### 1. docling-project/docling: https://github.com/docling-project/docling
- What: converts PDF/Office/HTML/images into one DoclingDocument with reading order, tables and per-element provenance (page_no + bbox). It includes structure-aware chunkers.
- What to borrow: `HybridChunker` (hierarchical chunks, split when oversized and merge when undersized against your embedding tokenizer), `chunk.meta.headings` as the section path, `contextualize()` to build the heading-prefixed text you embed, and `repeat_table_header=True` for long tables. Docs: https://docling-project.github.io/docling/concepts/chunking/
- Maturity (verified 2026-10-23): **69,406 stars, 5,160 forks, last push 2026-10-23, MIT**. README has run steps (`pip install docling`, `docling <url>`, VLM pipeline flag). Hosted in LF AI & Data. Releases are frequent: v2.141.0 (10-20) added Nemotron 3.5 Parse, v2.142.0 (10-22) bounded work on untrusted model output. Known users: IBM runs it as a managed service, "Docling for IBM watsonx" (IBM post 2026-10-21).
- Best for: **Devs and Architects** (default parser + chunker layer with provenance).

### 2. feyninc/chonkie (README still uses chonkie-inc links, and the old path still serves the README): https://github.com/feyninc/chonkie
- What: a lightweight chunking library. Token, Fast (SIMD), Sentence, Recursive (markdown recipe), Semantic, **Late**, Code, Neural, Slumber (LLM), **Table** chunkers, plus refineries (overlap, embeddings) and a Pipeline API. It can also run as a self-hosted REST server (`chonkie serve`).
- What to borrow: the Pipeline pattern (`recursive(markdown) -> semantic -> overlap -> embeddings`) for quick A/B of chunkers on your eval set, and `LateChunker` to test late chunking without writing it yourself. A TS sibling exists (feyninc/chonkiejs, 368 stars) for the TypeScript side.
- Maturity (verified): **4,802 stars, 364 forks, last push 2026-10-23, MIT**. README has install + usage + server steps. Speed/size benchmarks come from the authors (BENCHMARKS.md). No named production users in the README.
- Best for: **Devs** (chunker experiments, swapping strategies in minutes).

### 3. Ontos-AI/knowhere: https://github.com/Ontos-AI/knowhere
- What: document parsing + "navigable memory". Hierarchy reconstruction, a Vision track (page understood by a VLM) and a Text track that both produce one chunk/metadata schema, with page citations, linked assets, cross-doc relations, and agent tools over MCP. It uses MinerU as the V1 PDF extractor.
- What to borrow: the "two tracks, one contract" idea. Whatever parser you use, every chunk has the same schema (doc, section path, source pages, assets), so retrieval and citation don't depend on the parser.
- Maturity (verified): **3,743 stars, 338 forks, last push 2026-10-22, created 2026-04-30, Apache-2.0**. README has a Quick Start (uv sync, alembic, api/worker) and a Docker Compose self-host repo. Caveats: benchmark claims (+36% first-try accuracy) are **internal evaluation**. **Telemetry is on by default** (`TELEMETRY_ENABLED=false` turns it off). Young project.
- Best for: **Architects** (schema and design reference). Pilot it carefully, not as a production default yet.

---

## Sources

- [docling](https://github.com/docling-project/docling)
- [chonkie](https://github.com/feyninc/chonkie)
- [knowhere](https://github.com/Ontos-AI/knowhere)