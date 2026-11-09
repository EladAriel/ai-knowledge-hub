# METH-068: Parsy: parsing harness distilled into one model (reconstruction check)

## Summary

Aleph Alpha traced most wrong answers to parsing (tables whose numbers lost row/unit); the harness rebuilds each page from the parse and a vision judge compares it to the original.

## Details

Pages that fail are re-parsed or go to a human; no labels needed since the page is the ground truth. Distilled model: 87.9 on ParseBench vs 86.0 for the teacher harness, hundreds of thousands of pages/day on one H100, 10-100x cheaper per page. Found 145 ParseBench pages with questionable ground truth. Parsy isn't open: borrow the method, not the model. Adopt: Architects keep a bounding box on every parsed element (exact-spot citations); Product shows a per-page quality score and sends only low scorers to review; Devs rebuild a sample of pages in CI and compare.

## Content

**1. [Parsy: Aleph Alpha distills a parsing pipeline into one model](https://aleph-alpha.com/en/blog/parsy-distilling-an-agentic-parsing-harness/)**
- **The problem:** in customer projects, they traced most wrong answers back to parsing. The usual failure was tables where every number was extracted but lost its row or unit.
- **The fix:** their pipeline rebuilds each page from the parsed output and puts it next to the original. A vision model then compares the two. Pages that fail get parsed again or go to a person. No labels are needed, because the original page is the answer key.
- **The model:** they trained one model to copy that pipeline.
  - It scores 87.9 on ParseBench, versus 86.0 for the pipeline it learned from.
  - One H100 GPU handles hundreds of thousands of pages a day.
  - It costs 10 to 100 times less per page.
- **Honesty points:** they found 145 ParseBench pages with questionable answer keys, plus a leaderboard error that LlamaIndex then fixed.
- **Caveat:** Parsy isn't open, so borrow the method, not the model.
- Adopt for:
  - *Architects:* keep a bounding box (the element's position on the page) on every parsed element, so citations can highlight the exact spot.
  - *Product:* show a quality score for each page, and send only low scorers to human review.
  - *Devs:* in CI, rebuild a sample of pages from the parsed output and compare them to the originals.

## Sources

- [Aleph Alpha: Parsy](https://aleph-alpha.com/en/blog/parsy-distilling-an-agentic-parsing-harness/)