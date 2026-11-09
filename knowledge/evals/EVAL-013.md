# EVAL-013: Eval: regression suite from past production failures

## Summary

Versioned cases, each a real failure; a change can't ship if a previously passing case fails.

## Details

1) Last 30 days of thumbs-down/escalations/incidents; keep top 30-50 by frequency x severity (1-2 h). 2) Tag failed stage: stale source, never ingested, retrieval miss, permission, answer writing, tool (MemDerive: most memory failures were facts never retrieved) (1 h). 3) Checks: must cite X / must not cite Y / must refuse; code first, cheap judge for the rest (2 h). 4) 3-5 paraphrases per case + random everyday queries as negative control (1 h). 5) Freeze tool outputs and corpus version; CI fails on regressions (1-2 h). 6) Every new failure gets a case before its fix merges.

## Content

## 4. Simple eval technique: regression suite from past failures

**What it is:** A versioned set of test cases where every case is a real production failure. Each case keeps its input, its recorded context and a checkable expected behavior. A change ships only if no previously passing case starts failing.

**Steps (under a day)**
1. **Collect (1–2 h):** Gather the last 30 days of thumbs-down with comments, escalations, incident-linked sessions and failure clusters. Keep the top 30–50 by frequency × severity.
2. **Tag the stage (1 h):** Mark each case as stale source, never ingested, retrieval miss, permission, generation or tool. [MemDerive](https://arxiv.org/abs/2610.25373) found most memory failures were "ungathered": the state existed but was not retrieved.
3. **Write assertions (2 h):** For example: "must cite doc X," "must not cite doc Y," "must say Owner role only," "must refuse." Prefer code checks and use a cheap judge for the rest.
4. **Add paraphrases and a control slice (1 h):** Add 3–5 held-out paraphrases per case so you test the fix, not one exact string. Add random normal queries so a fix can't take over unrelated traffic (INO used 1,400).
5. **Freeze and gate (1–2 h):** Store the recorded tool outputs and the corpus version, and version the suite (for example, a Kitaru cohort). CI fails if any previously passing case now fails.
6. **Rule:** Every new production failure gets a case before its fix merges.

**What it catches:** Regressions from model swaps, prompt edits, re-chunking, re-indexing and connector changes. It also catches corrections that are no longer retrieved and stale facts that come back. Add a few "wrong user must not see doc" cases and it catches permission leaks too.

**Who runs it:** Product owns intake, severity and expected behaviors. Devs own the harness, replay and CI gate. Architects own the snapshot contract and the privacy rules for stored traces.

---

## Sources

- [MemDerive](https://arxiv.org/abs/2610.25373)