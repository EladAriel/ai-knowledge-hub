# EVAL-012: MASIF: successful agent runs hide failures

## Summary

1,828 multi-agent traces: hidden failures in 54.3% of successful traces and 75.2% of failed ones.

## Details

Watching only outcomes misses more than half the process problems (LLM-labeled with human spot checks). Keep traces of every step; report a hidden-failure rate next to task success; add per-step checks for retries, ignored tool errors and contradictory facts.

## Content

### [MASIF: "successful" agent runs often hide implicit failures](https://arxiv.org/abs/2610.25852)
- **What:** HKUST and Adobe annotated 1,828 multi-agent traces across 9 setups. An implicit failure is a local error that gets corrected, bypassed or carried forward. They appeared in 54.3% of successful traces and 75.2% of failed ones.
- **Why it matters:** Outcome-only monitoring misses process problems in more than half of passing runs, and those become tomorrow's regressions. Limits: the labels come from an LLM (with human audits), and the training method built on them shows only "some gains."
- **Effort:** med
- **Adopt for:**
  - **Architects:** Keep step-level traces, not just final answers, with clear retention rules.
  - **Product:** Report an implicit-failure rate next to task success.
  - **Devs:** Add per-span checks for retries, ignored tool errors and contradicted facts.

## Sources

- [MASIF](https://arxiv.org/abs/2610.25852)