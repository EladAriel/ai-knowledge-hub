# EVAL-016: Eval: answer-span containment and chunk integrity

## Summary

Check whether each gold answer span sits whole inside one chunk and in the retrieved top-k; lint fragments and broken tables.

## Details

1) 50-100 gold Q&A with answer offsets in the parsed text (+ table and page-break questions). 2) locate_span: exact then whitespace-normalized; not found = parse-fidelity failure. 3) Keep (doc_id,start,end) per chunk. 4) Containment rate and split rate. 5) Retrieved containment@k vs recall@k (gap = right doc, broken piece). 6) Lints: fragment rate, tables missing header, fused headings. 7) CI per chunker/parser config: containment >= 95%, fragment rate \<= 2%, no drop vs last release.

## Content

## (D) Eval technique: answer-span containment and chunk integrity test

- **What:** for each gold question, mark the exact **answer span** in the parsed document (character offsets). Then check (a) whether any single chunk contains the whole span (**containment rate**), (b) whether the retrieved top-k includes a chunk that contains it (**retrieved containment@k**), and (c) structural integrity: tables split without a header, headings fused into body text, and chunks ending mid-sentence (**fragment rate**). It tests the chunker itself, before retrieval and generation get involved.
- **Sources:** span-to-chunk relevance mapping, where evidence spans are mapped to every chunk that contains them and overlapping chunks count as relevant, is from https://arxiv.org/abs/2610.31606 (2026-10-22). The fragment-rate check (stored claims that don't end in a full stop, 43% -> 1%) and the fused-heading detector are from the Akamai post above.

**Steps (under a day):**
1. Take 50-100 existing gold Q&A pairs (reuse the golden set from 10-17). For each one, store `doc_id` + the exact answer string, or better, char offsets in the *parsed* text. Add 10-20 table questions and 10 questions whose answer sits next to a page break.
2. Write `locate_span(doc, answer)`: find the span with exact match first, then whitespace-normalized match. Record cases where the span **cannot be found in the parse at all**. That is a parse-fidelity failure, not a chunking failure.
3. For each chunk, keep `(doc_id, start_char, end_char)` from the chunker. If your chunker doesn't give offsets, recover them by string search.
4. Compute **containment rate** = % of spans fully inside at least one chunk, and **split rate** = % of spans cut across 2+ chunks.
5. Run retrieval and compute **retrieved containment@k** = % of questions where a top-k chunk fully contains the span. Compare it with ordinary recall@k: a big gap means you retrieve the right doc but a broken piece of it.
6. Integrity lints over all chunks: % ending without terminal punctuation (fragment rate); table chunks whose first row is not a header row while the source table had one; chunks whose body starts with heading text (a heading fused into a paragraph); chunks with an empty heading path that should have one.
7. Run the full test for every chunker/parser config (for example fixed vs HybridChunker vs chonkie recursive). Put it in CI with thresholds, for example containment >= 95%, fragment rate <= 2%, and no drop compared with the last release.

- **What it catches:** answers split across chunk boundaries, tables cut without headers, headings glued to paragraphs, page-break fragments, parser text loss (span not found), and regressions when someone changes chunk size or swaps parsers. Before this, those failures only showed up as vague "bad answers".
- **Who runs it:** **Devs** build and run it in CI. **Architects** set the thresholds and make it a gate for any parser/chunker change. **Product** supplies the table and page-break questions from real user asks.

---

## Sources

- [span-to-chunk mapping](https://arxiv.org/abs/2610.31606)