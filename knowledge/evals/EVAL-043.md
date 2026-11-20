# EVAL-043: Eval: which stage broke first (stage-blame on 30 failed questions)

## Summary

A same-day eval you can start in under a day (Nov 19). Take 30 questions that got a wrong final answer. For each one, mark the first stage that broke: the document was never brought into the system; search missed it; it was found but cut from the top results; a permission filter blocked it; or the answer or its citation was wrong. Count the questions per stage and fix the biggest group first.

## Details

What it catches: effort going into the wrong layer. A quality score on the final answer hides whether the miss was ingestion, retrieval, ranking, permissions, or generation.

Start in under a day: export 30 failed questions, label the first broken stage in a spreadsheet, and rank the bars.

Who runs it: Product owns the weekly sample and the decision of which bar to fix first. Devs pull the traces and the retrieved sources for each question. Architects review whether permission blocks are being mis-labeled as missing content.

Related: EVAL-028 (RAGLog) finds a broken RAG stage from logs alone, with no hand labels. This eval is the manual version on your own failed questions. Complements today's end-to-end gates in PIPE-034.

## Sources

- No external link was recorded for this eval itself. Related public sources (see PIPE-034 and METH-184):
- [Vendor demos fool the people scoring them (gate, then score)](https://arxiv.org/abs/2611.24039)
