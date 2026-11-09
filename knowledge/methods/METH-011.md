# METH-011: CarryOn: An object-based context for long-lived agents

## Summary

Instead of saving the interaction history, the agent manages continuity around reusable task objects, keeping a verified record of the state.

## Details

The context is reorganized around the task deliverables, and a verified record of the state is kept instead of a summary or sliding window.

## Content

### 2. [CarryOn: An Object-Based Context for Long Agents](https://arxiv.org/abs/2610.18784)
[Project](https://ethannju.github.io/carryon)

- **What it is:** Instead of saving the interaction history, the agent manages the continuity around reusable task objects, and keeps an authenticated record of the state.
- **Why new:** This is not another summary or sliding window. The context is reorganized around the deliverables of the task.
- **Evidence:** In OSWorld 2.0 the partial score increased from 43.9 to 49.7, with 51.9% fewer toucans. In BrowseComp-Plus the accuracy increased by 7 points. The comparison is against Claude Opus 4.7 and against accepted summary methods, and there are ablations. The generality beyond computer-use and surfing has not yet been proven.
- **Scores:** Effectiveness 4/5, Hype 3/5.
- **Adjustment and effort:** Desktop agents and research agents that run for a long time. **high** effort.
- **Recommendation: Pilot** on long routes only, not on every chat.

## Sources

- [CarryOn: An object-based context for long-lived agents](https://arxiv.org/abs/2610.18784)
- [project](https://ethannju.github.io/carryon)