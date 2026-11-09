# METH-044: Padding to k: schema minimums make models invent list items

## Summary

With 'at least k items' in a JSON schema, over-long lists rose from 34.5% to 55.4% (8 open models, 558 docs).

## Details

Hard to catch: about half the padded items are real text copied from the doc. Re-asking with the validation error makes it worse; 'up to k' also raises over-counting. Ban minItems on extraction schemas, make zero items valid, CI test with docs holding 0 or 1 items; track invented facts separately from missed facts. Pre-registered, code and data public.

## Content

**1. [Padding to k: schema minimums make models pad extraction lists](https://arxiv.org/abs/2610.30997)**
- If your JSON schema says "at least k items" and the document has fewer, models make up the difference. Across 8 open-weight models and 558 real documents, lists longer than the true count rose from 34.5% to 55.4%. The study was registered in advance, and its [code and data](https://github.com/AbhishekBarali/padding-to-k) are public.
- It's hard to catch. About half the padded items are real text copied from the doc, so a simple "does this appear in the source" check lets them through.
- Fixes only partly work. Re-asking the model with the validation error makes padding much worse, and writing "up to k" in the prompt also raises over-counting.
- Adopt for:
  - *Architects:* ban `minItems` on extraction schemas in your data contract, and make "zero items" a valid answer.
  - *Product:* track invented facts as a separate metric from missed facts.
  - *Devs:* add a CI test with docs that hold 0 or 1 items, and check that the extractor returns no more than that.

## Sources

- [Padding to k](https://arxiv.org/abs/2610.30997)
- [code and data](https://github.com/AbhishekBarali/padding-to-k)