# METH-096: Airlock: Bounding the Multi-Agent Blast Radius (EdgeCitadel)

## Summary

Runtime for multi-agent systems: permissions shrink from parent to child, a provenance DAG records who consumed information from whom, and on an alert the system isolates only the contaminated branches instead of stopping the whole workflow.

## Details

Partly a rebrand of taint tracking and least privilege; the new piece is connecting them to surgical isolation at runtime, with a min-cut that accounts for deadlocks. Fit: multi-agent systems that take real-world actions. Effort: medium to high, but provenance logging alone is easy to adopt. Recommendation: Pilot. Code: EdgeCitadelTeam/EdgeCitadel.

## Sources

- [Airlock (arXiv)](https://arxiv.org/abs/2611.06727)
- [EdgeCitadel](https://github.com/EdgeCitadelTeam/EdgeCitadel)
