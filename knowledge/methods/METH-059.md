# METH-059: CoSA: an attack created from a combination of skills

## Summary

Each skill can be correct on its own, and their combination still violates the policy.

## Content

**2. [CoSA: an attack created by combining skills](https://arxiv.org/abs/2610.35082)**, and next to it [NVIDIA SkillSpector](https://github.com/NVIDIA/SkillSpector)
- **What is it:** Each skill can be correct on its own, and their combination still violates the policy. For example, a product created for one purpose is used for another purpose without the appropriate authorization. In the CoSA-Bench test, adding up to 5% skills to the pool increased the violation rate from 35% to 58%.
- **Why new:** Scanning each skill separately, which SkillSpector does, does not catch this problem. The new one is a guard at the harness level, which checks the flow of information and authorization before any action that has consequences.
- **Evidence:**
  - The guard downloaded a... The RCA article is an empirical study with baselines. At Anthropic there is only a doubt claim, but the assessment is based on before and after measurement.
- **Scores:** Effectiveness 4/5, Hype 3/5.
- **Compatibility:** Any product with orchestrator and subagents. **medium** effort, and a prerequisite is an end-to-end eval set.
- **Recommendation: Adopt** As a method: first build a baseline of one loop, and only then add orchestration. This aligns with the multi-agent study from 21.10.

## Sources

- [CoSA: an attack created from a combination of skills](https://arxiv.org/abs/2610.35082)
- [NVIDIA SkillSpector](https://github.com/NVIDIA/SkillSpector)
