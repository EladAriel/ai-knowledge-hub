# EVAL-003: Memory evals should check the store (FEB-30, Bemula)

## Summary

Grading only final answers disagreed with checking the memory store by 16 points; no memory system passed forget requests above 1.5%.

## Details

FEB-30: tested system picked the right memory operation (create/update/reinforce/supersede) only 20% of the time. Bemula: across six memory systems none passed >1.5% end-to-end on deletion (left data extractable or deleted too much). Devs: ingest A, then 'A changed to B', then assert on stored contents, not just the answer; require versioned, supersedable facts and a delete path covering derived copies.

## Content

### 4. Agent-memory evals are measuring the wrong thing: [FEB-30](https://arxiv.org/abs/2610.22209) and [Bemula](https://arxiv.org/abs/2610.18052) (arXiv, Oct 13–15) | Effort: **med**
- **FEB-30:** it checks the memory store directly. Grading only the final answers ("extrinsic") disagreed with checking the store itself ("intrinsic") by 16 points on average. The system tested picked the right memory operation (create, update, reinforce, or supersede) only **20%** of the time. Limitations: 30 fact trajectories, one system tested.
- **Bemula:** it tests forget requests. Across six mainstream memory systems, none passed more than **1.5%** end to end: they either left the data extractable or deleted too much ([code](https://github.com/Nboxff/bemula-benchmark)).
- **Why it matters:** a company brain must handle "this fact changed" and "delete this" (GDPR-style requests). Good answers can hide a broken store.
- **Adopt for:**
  - *Architects:* require facts that are versioned and can be superseded (validity windows), plus a delete path that also covers derived copies.
  - *Product:* add "freshness after a change" and "deletion honored" to the success metrics.
  - *Devs:* write tests that ingest A, then ingest "A changed to B", then assert on the stored contents, not just on the answer.

## Sources

- [FEB-30](https://arxiv.org/abs/2610.22209)
- [Bemula](https://arxiv.org/abs/2610.18052)
- [code](https://github.com/Nboxff/bemula-benchmark)