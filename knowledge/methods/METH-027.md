# METH-027: Tether: withdraw memories when their sources break

## Summary

Record which source versions each memory depends on; plain memory let 62% of broken-source answers out, Tether 0.3% with 37% fewer checks.

## Details

Mem0 let 42% through, A-Mem/Graphiti 9%. Synthetic worlds; misses rise to 9-22% when the dependency appears in another session. Make 'derived from (doc, version)' required on cached answers; on source version change invalidate everything built from it.

## Content

### [Tether: memories that outlive their reasons](https://arxiv.org/abs/2610.25123) ([code](https://github.com/xiaoqi-7/tether-fallout))
- **What:** When it writes a memory, Tether records the exact source versions each verdict depends on. At read time, it withdraws any verdict whose support has failed.
- **Numbers vs baseline:** With plain fact memory, the agent published 62% of objects whose failure lay upstream. Tether let through 0.3%, using 37% fewer checks than re-verifying everything. Mem0 let through 42% and A-Mem/Graphiti 9%.
- **Why it matters:** Policies change and derived answers silently go stale. Limits: the worlds are synthetic, and when dependencies arrive in a different session, misses rise to 9.4–22.1%. This continues the provenance theme from earlier runs.
- **Effort:** med
- **Adopt for:**
  - **Architects:** Make "derived from (doc, version)" a required field on cached answers.
  - **Product:** Choose which answers must never be served stale (pricing, policy, access).
  - **Devs:** When a source version changes, invalidate everything that depends on it.

---

## Sources

- [Tether](https://arxiv.org/abs/2610.25123)
- [code](https://github.com/xiaoqi-7/tether-fallout)