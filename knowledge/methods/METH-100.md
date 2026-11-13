# METH-100: PULSAR: production enterprise RAG over page images (ColQwen3-4B) instead of OCR

## Summary

Mubadala indexes page images of pitch decks and board packs with ColQwen3-4B (ColPali-style late interaction): 78k documents, ~2.4M pages, live since March 2026. Reported ~20x cheaper ingestion per page than the OCR pipeline it replaced and facts-in-top-5 up from 0.271 to 0.733 on 75 expert questions. EMNLP 2026 Industry track.

## Details

Results: ingestion ~20x cheaper per page (estimated from call counts); 73% of the old pipeline's chart-description calls produced output that was thrown away; on 75 expert-written questions, finding the right facts in the top 5 went from 0.271 to 0.733.
Ingestion tricks: per-document and per-page hashes so only changed pages are re-embedded; separate priority queues so live uploads jump ahead of bulk syncs; restart from the last saved page after a crash; a document shows up in search only after every page is saved; median change-to-searchable 2 s, 95% under 43 s.
Stated limits: index tuning measured on a public benchmark, not their own documents; only one baseline.
Effort: medium to high.
Adopt for: Architects (freshness target; 'searchable only once fully saved' in the ingestion contract); Product (for chart-heavy content, test page images vs OCR on 50 expert-written questions); Devs (page-level hashes and a 'document complete' marker).
Insights #2 (ENGRAM) and #3 (Context Mode 2.0) from the same brief are separate items: METH-112 and METH-113.

## Content

**1. [PULSAR: enterprise RAG over page images, in production](https://arxiv.org/abs/2608.28572)**, EMNLP 2026 Industry track
- **What it is:** the investment firm Mubadala indexes pictures of each page of its pitch decks and board packs, instead of extracting the text with OCR. It uses ColQwen3-4B, which stores many vectors per page (ColPali-style). That covers 78k documents and about 2.4M pages, live since March 2026.
- **Results:**
  - Ingestion costs about 20 times less per page than the OCR pipeline it replaced, though that figure is estimated from call counts.
  - 73% of the old pipeline's calls to describe charts produced output that was thrown away.
  - On 75 questions written by experts, finding the right facts in the top 5 went from 0.271 to 0.733.
- **Ingestion tricks worth copying:**
  - A hash of each document and each page, so only changed pages get re-embedded.
  - Separate priority queues, so live uploads jump ahead of bulk syncs.
  - Restart from the last saved page after a crash.
  - A document shows up in search only after every one of its pages is saved.
  - Median time from a change to it being searchable is 2 seconds, and 95% of changes take under 43 seconds.
- **Limits they state:** the index tuning was measured on a public benchmark, not their own documents, and they compared against only one baseline.
- Effort: medium to high.
- Adopt for:
  - *Architects:* set a target for how fast a change becomes searchable, and make "searchable only once fully saved" part of the ingestion contract.
  - *Product:* for chart-heavy content like decks, finance reports or engineering drawings, test page images against your OCR on 50 expert-written questions.
  - *Devs:* add page-level hashes and a "document complete" marker to your ingestion.

## Sources

- [PULSAR (arXiv 2608.28572)](https://arxiv.org/abs/2608.28572)
