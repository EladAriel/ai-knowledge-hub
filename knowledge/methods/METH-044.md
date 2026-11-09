# METH-044: Padding to k: schema minimums make models invent list items

## Summary

With 'at least k items' in a JSON schema, over-long lists rose from 34.5% to 55.4% (8 open models, 558 docs).

## Details

Hard to catch: about half the padded items are real text copied from the doc. Re-asking with the validation error makes it worse; 'up to k' also raises over-counting. ….

## Sources

- [Padding to k](https://arxiv.org/abs/2610.30997)
- [code and data](https://github.com/AbhishekBarali/padding-to-k)
