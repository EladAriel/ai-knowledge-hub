# METH-068: Parsy: parsing harness distilled into one model (reconstruction check)

## Summary

Aleph Alpha traced most wrong answers to parsing (tables whose numbers lost row/unit); the harness rebuilds each page from the parse and a vision judge compares it to the original.

## Details

Pages that fail are re-parsed or go to a human; no labels needed since the page is the ground truth. Distilled model: 87.9 on ParseBench vs 86.0 for the teacher harness, hundreds of thousands of pages/day on one H100, 10-100x cheaper per page. Found 145 ParseBench pages with questionable ground truth. Parsy isn't open: borrow the method, not the model. Adopt: Architects keep a bounding box on every parsed element (exact-spot citations); Product shows a per-page quality score and sends only low scorers to review; Devs rebuild a sample of pages in CI and compare.

## Sources

- [Aleph Alpha: Parsy](https://aleph-alpha.com/en/blog/parsy-distilling-an-agentic-parsing-harness/)
