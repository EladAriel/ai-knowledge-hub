# TOOL-044: Repos: opendataloader-pdf, Lightfoot-GraphRAG, MIRIX

## Summary

A PDF-to-Markdown/JSON parser with page positions, the Lightfoot GraphRAG code, and six-type agent memory that keeps original records.

## Details

opendataloader-pdf (opendataloader-project/opendataloader-pdf; ~30k★, Apache-2.0, v2.5.21 the same day): keeps each element's position, reading order and tables, and filters headers/footers; hybrid mode adds OCR and complex tables (needs Java 11+; Python/Node/Java SDKs). Borrow element positions for citations and sending only hard pages to a model. Caveat: first-place result is from the authors' own benchmark; hybrid mode relies on Docling—test on your files. Best for Devs. Lightfoot-GraphRAG (udayallu-ml/Lightfoot-GraphRAG): code behind the Lightfoot insight; provenance in SQLite or Postgres and 82 tests including exact-deletion tests. Very early (created Nov 7, 0 stars, one author, MIT)—copy the ideas, don't depend on it. Best for Architects. MIRIX (Mirix-AI/MIRIX; ~3.5k★, Apache-2.0, pushed the day before, Docker quick start): agent memory split across six types, each run by its own agent; keeps full original records, optional Neo4j graph linking facts back to them, offline job merges duplicates without rewriting records. MIRIX-2.0 paper (arXiv 2611.12068) reports 91.4% on LoCoMo, self-reported. Borrow search with fixed budgets and original records as source of truth. Best for Devs and Architects.

## Sources

- [opendataloader-pdf](https://github.com/opendataloader-project/opendataloader-pdf)
- [Lightfoot-GraphRAG](https://github.com/udayallu-ml/Lightfoot-GraphRAG)
- [MIRIX](https://github.com/Mirix-AI/MIRIX)
- [MIRIX-2.0 paper](https://arxiv.org/abs/2611.12068)
