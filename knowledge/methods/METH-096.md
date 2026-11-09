# METH-096: Airlock: Bounding the Multi-Agent Blast Radius (EdgeCitadel)

## Summary

Runtime for multi-agent systems: permissions shrink from parent to child, a provenance DAG records who consumed information from whom, and on an alert the system isolates only the contaminated branches instead of stopping the whole workflow.

## Details

Partly a rebrand of taint tracking and least privilege; the new piece is connecting them to surgical isolation at runtime, with a min-cut that accounts for deadlocks. Fit: multi-agent systems that take real-world actions. Effort: medium to high, but provenance logging alone is easy to adopt. Recommendation: Pilot. Code: EdgeCitadelTeam/EdgeCitadel.

## Content

**3. [Airlock: Bounding the Multi-Agent Blast Radius](https://arxiv.org/abs/2611.06727)** ([EdgeCitadel Code](https://github.com/EdgeCitadelTeam/EdgeCitadel))
- **What it is:** runtime for multi-agent systems. Permissions are reduced from parent to child, and the DAG of provenance records who consumed information from whom. When an alert is received, the system isolates only the contaminated branches, instead of stopping the entire workflow.
- **Why new:** Partial rebrand of taint tracking and least privilege. The innovation is their connection to surgical isolation at runtime, with min-cut that takes deadlocks into account.
- **Compatibility:** Multi-agent systems operating in the real world. Medium to high effort, but log provenance alone is easy to adopt.
- **Recommendation: Pilot.** Code: EdgeCitadelTeam/EdgeCitadel.

## Sources

- [Airlock (arXiv)](https://arxiv.org/abs/2611.06727)
- [EdgeCitadel](https://github.com/EdgeCitadelTeam/EdgeCitadel)