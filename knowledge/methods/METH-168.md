# METH-168: Antigravity /teamwork: a team of agents where each role has a separate context

## Summary

Google's multi-agent system: Sentinel coordinates; Project Orchestrator hands work to a fresh agent between milestones; Explorers only read, and Workers work on paths that don't overlap; Critic and Success Auditor check the artifact from a clean context, without seeing the thinking of whoever produced it. Recommendation: Pilot, starting with two cheap principles. Effort: medium, and you can apply the pattern without Antigravity. 193 points on HN.

## Details

Orchestration with a verifier is a known idea. What's new is a documented, productized role architecture: context separation is set in advance, not patched after the fact; the coordinator is replaced on purpose so its context doesn't wear out; checking relies on external tools such as Lean 4, test suites that weren't changed, simulators and hardware meters; at runtime the system chooses among work templates written in natural language, and the templates improve from transcripts of earlier runs. Evidence, from Google's blog with academic partners: a formal Lean proof of the Courtade–Kumar conjecture, and 95% accuracy identifying molecular structure from NMR. The math proof can be checked in Lean. There is no controlled comparison to a single agent, so it isn't clear how much each component contributes. Effectiveness 4/5, hype 3/5. Fit is high for any product with long tasks, such as migrations, research or reports. Pilot first on two cheap principles: a critic that receives only the artifact, and a handoff to a fresh agent between stages. This continues Antigravity Orchestrator from Nov 13, and lines up with yesterday's finding on cleaning history at handoff (METH-164).

## Sources

- [Antigravity /teamwork blog](https://research.google/blog/advancing-science-engineering-with-antigravitys-teamwork-feature/)
- [Antigravity teamwork roles doc](https://antigravity.google/docs/teamwork/)
