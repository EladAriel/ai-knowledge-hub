# METH-164: Cleaning a harmful agent's history when the world still contains the error

## Summary

Freeze an agent mid-task, edit the history or the world state, and test how a model that continues the work recovers. The question is what you should write about mistakes when you compact, repair, or hand off. Recommendation: Adopt as a check of the compaction and handoff mechanism. Effort: low.

## Details

Earlier work cleaned history against a world that doesn't change. This paper (arXiv 2611.14654) shows that the same true content can help or hurt, depending on the wording and on what actually happened in the world. Evidence: on AgentCE-Bench, a true note next to the saved mistake raised recovery from 51% to 66%; a fake "perfect action" lowered it from 50% to 44%. On AppWorld, a success confirmation when the actual effect was missing lowered success from 45% to 28%. The result held on 6 to 7 of 8 continuing models. There is no repo. Effectiveness 4/5, hype 1/5. Fit is direct for any product that compacts context or hands a task between models. The practical rule: don't delete mistakes; add a true correction next to them. A Nov 15 review ties this to Antigravity /teamwork handoff (METH-168).

## Sources

- [Cleaning a harmful agent's history](https://arxiv.org/abs/2611.14654)
