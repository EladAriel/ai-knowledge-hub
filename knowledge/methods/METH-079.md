# METH-079: Zep Agent Skills: procedures compiled from verified runs (procedural memory)

## Summary

Every task run is recorded as a trace; only successful runs confirmed by a tool, customer or outside system are compiled into a versioned SKILL.md, each step citing its source runs, with a trust score moved by verified wins/failures.

## Details

Results: skills built  memory). Terms: procedural memory = stored 'how to do X' steps; attempt family = one task attempt plus its retries, counted as one piece of evidence. Adopt for: Architects: treat 'what counts as verified' as a data contract (approved verifiers per task type). Product: pick 2–3 repeated workflows (refunds, onboarding tickets) and track pass rate before/after. Devs: write traces with outcome + verifier fields now, even before a skill compiler exists. Harness (Nov 3 digest filter): add outcome and verified_by (which gate or CI approved the run) fields to the harness run log; these 'verified' runs are the basis for learning from successful runs and for comparing models. Effort small to medium; note it's Zep's internal benchmark.

## Content

**1. [Zep Agent Skills: procedures learned from verified runs](https://arxiv.org/abs/2611.01386)** ([docs](https://help.getzep.com/agent-skills))
- **How it works:** every task run is recorded. Only successful runs confirmed by a tool, a customer or an external system get turned into a versioned SKILL.md. Each step cites the runs it came from, and each skill carries a trust score that goes up or down with verified wins and failures.
- **Results:** skills built from a stronger model's runs raised weaker models' pass rates by 4.5 to 18.8 points.
- **Caveats:** Zep ran these tests himself, and most of the gain is on tasks the stronger model had already solved.
- **Pattern:** this is the third time skills have come up as memory, after Airbnb and Neo4j agent memory.
- Adopt for:
  - *Architects:* decide which checks count as verifying a run for each task type, and write that down as a contract.
  - *Product:* pick 2-3 repeated workflows, like refunds or onboarding, and track pass rates before and after.
  - *Devs:* start recording the outcome and who confirmed it on every run now, even with no skill builder yet.

2. **Each run is recorded with the result and with who approved it**: add to the run log the `outcome' and `verified_by' fields (which gate or CI approved the run). These are "verified" runs, and they are the basis for learning from successful runs and for comparing models.
   - **Effort:** Small to medium.
   - **Source:** [Zep Agent Skills](https://arxiv.org/abs/2611.01386). Note that this is an internal Zep benchmark.I put the first one in the 9:00 queue. I filtered human-gate and policy-ceiling, because they are plugins of a specific vendor, and your gates already cover their role.

## Sources

- [Zep Agent Skills (arXiv)](https://arxiv.org/abs/2611.01386)
- [Zep Agent Skills docs](https://help.getzep.com/agent-skills)