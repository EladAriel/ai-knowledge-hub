# METH-047: AfterDeleteBench: deleted memory survives in derived state

## Summary

Deleting a source leaves its content in summaries and extracted facts: one query recovered the secret ~2/3 of the time.

## Details

Scattered fragments let models rebuild it 62-99% of the time. Fix: provenance-aware closure (delete everything derived from a source). Every extracted entity/summary stores source IDs; ….

## Sources

- [AfterDeleteBench](https://arxiv.org/abs/2610.31366)
