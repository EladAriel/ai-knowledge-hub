# METH-079: Zep Agent Skills: procedures compiled from verified runs (procedural memory)

## Summary

Every task run is recorded as a trace; only successful runs confirmed by a tool, customer or outside system are compiled into a versioned SKILL.md, each step citing its source runs, with a trust score moved by verified wins/failures.

## Details

Results: skills built from a stronger model's runs raised weaker models' pass rates by 4.5–18.8 points. Caveats: Zep ran the tests itself; most of the gain is on tasks the stronger model had already solved. Pattern: third time skills show up as memory (after Airbnb's portable skill and Neo4j agent memory). Terms: procedural memory = stored 'how to do X' steps; attempt family = one task attempt plus its retries, counted as one piece of evidence. Adopt for: Architects: treat 'what counts as verified' as a data contract (approved verifiers per task type). Product: pick 2–3 repeated workflows (refunds, onboarding tickets) and track pass rate before/after.

## Sources

- [Zep Agent Skills (arXiv)](https://arxiv.org/abs/2611.01386)
- [Zep Agent Skills docs](https://help.getzep.com/agent-skills)
