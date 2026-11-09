# TOOL-015: Small parser models: OCRia-1, Nemotron 3.5 Parse, SoMark OXR

## Summary

LlamaIndex OCRia-1 (4B): 87.4 on ParseBench vs 75.3 next (LlamaIndex's own benchmark), no bounding boxes. NVIDIA Nemotron 3.5 Parse (631M, open, commercial use): layout, bounding boxes, reading order; supported by Docling. SoMark OXR (1.3B): claims #1 on several benchmarks, very young, unclear license.

## Content

### 2. Small parser VLMs moved fast this week: OCRia-1 (4B), Nemotron 3.5 Parse (631M, open), OXR (1.3B, open)
- URL: https://www.llamaindex.ai/blog/parse-ocria-1 (LlamaIndex, 2026-10-22; tech report: https://www.llamaindex.ai/ocria/ocria-1-technical-report.pdf)
- What: OCRia-1 is a 4B VLM that powers LlamaParse. The vendor reports **87.4** overall on ParseBench, **12.1 points** ahead of the next model (LightOnOCR-3-4B, 75.3). Its charts score is 85.1 against 66.1, and its formatting score is 83.4 against 67.9. It was trained with SFT + RLVR on 100k+ pages. Caveat from the tech report: it **does not output bounding boxes**, so ParseBench's visual-grounding dimension was left out. I did not see open weights in the post.
- Same week: NVIDIA **Nemotron 3.5 Parse** (631M, open, commercial use; outputs layout classes, bounding boxes and reading order; https://huggingface.co/nvidia/Nemotron-3.5-Parse). It is already a supported VLM in Docling v2.141.0 (2026-10-20, per the CHANGELOG). The same NVIDIA release says adding their reranker cut agent tokens per query by about **14%** (https://huggingface.co/blog/nvidia/nemotron-retriever-world-class-agentic-retrieval). **SoMark OXR** (1.3B) claims #1 on olmOCR-Bench, OmniDocBench and DocParsingBench and has a pluggable layout model (https://github.com/SoMarkAI/OXR; 250 stars, created 2026-10-05, license shows as NOASSERTION, arXiv "coming soon").
- Why it matters: page-to-Markdown/HTML parsing with tables and charts is now cheap enough to run on every page. But every leaderboard here is vendor-run, and ParseBench is LlamaIndex's own benchmark. Bounding boxes are what let you cite back to a page region, and not every model gives them.
- Adopt for:
  - Architects: put the parser behind an interface (Docling already wraps several VLMs). Store parser name + version on each doc so you can re-parse later. Require bbox/page provenance if you need region-level citations.
  - Product: tables and charts are where users ask for numbers. Treat "chart-to-table" as a feature you can ship for finance and insurance docs.
  - Devs: try Docling's Nemotron 3.5 Parse pipeline against your current parser on your own pages, and score them with your own checks, not vendor charts.

## Sources

- [OCRia-1](https://www.llamaindex.ai/blog/parse-ocria-1)
- [Nemotron 3.5 Parse](https://huggingface.co/nvidia/Nemotron-3.5-Parse)
- [SoMark OXR](https://github.com/SoMarkAI/OXR)
