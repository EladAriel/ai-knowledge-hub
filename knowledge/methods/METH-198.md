# METH-198: Skills wear out when the model rewrites them without feedback (Adopt-check)

## Summary

More and more systems let the model "improve" skill files on its own. After 30 rewrite rounds with no task and no judge, every model dropped on every benchmark, by an average of 15 points on SkillsBench. The rewrite pulls the skill toward what the model already knows, and the unique knowledge is erased first. SkillDiff tags with [FOCUS] the parts the model would not have written on its own, and adds 4.8 points. The value of a skill is exactly what the model does not know. This follows yesterday's item on GEPA and harness evolution (METH-196): evolution works only with real feedback. Recommendation: Adopt-check. Do not allow automatic rewriting of skills without an eval, and consider FOCUS tags. Effort: low. arXiv 2611.25534; code: LitaoGuo/How-Self-Evolution-Reshapes-Skills.

## Details

From the Nov 22 methods digest.

## Sources

- [Skills wear out without feedback](https://arxiv.org/abs/2611.25534)
- [LitaoGuo/How-Self-Evolution-Reshapes-Skills](https://github.com/LitaoGuo/How-Self-Evolution-Reshapes-Skills)
