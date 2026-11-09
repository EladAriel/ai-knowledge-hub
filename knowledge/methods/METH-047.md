# METH-047: AfterDeleteBench: deleted memory survives in derived state

## Summary

Deleting a source leaves its content in summaries and extracted facts: one query recovered the secret ~2/3 of the time.

## Details

Scattered fragments let models rebuild it 62-99% of the time. Fix: provenance-aware closure (delete everything derived  about its facts.

## Content

**4. [AfterDeleteBench: deleted memory survives in derived state](https://arxiv.org/abs/2610.31366)**
- When you delete a source record, the summaries and extracted facts built from it can still carry its content. A single query recovered the "deleted" secret about two-thirds of the time, and even scattered fragments let the model rebuild it 62–99% of the time.
- In their tests, the fix was to delete everything derived from a source along with the source itself. The authors call this provenance-aware closure. It extends the recent "keep derived layers rebuildable" theme to "keep them deletable too."
- Adopt for:
  - *Architects:* make every extracted entity and summary store the source IDs it came from, so a delete reaches everything built from that source.
  - *Product:* set a right-to-be-forgotten deadline that covers derived data too.
  - *Devs:* add a test that deletes a doc and then asks the agent about that doc's facts.

## Sources

- [AfterDeleteBench](https://arxiv.org/abs/2610.31366)