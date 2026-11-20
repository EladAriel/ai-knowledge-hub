# METH-165: EvoX and MultiLoop: harness optimization, with Outcome Grounding as the piece to try

## Summary

A new framing of the existing harness-optimization line. Worth taking the Contrast comparison setup and MultiLoop's finding. Recommendation: Watch. Effort: high. A Nov 15 review adds that Outcome Grounding is the component to try first.

## Details

Evidence, from the authors' own comparison: EvoX (arXiv 2611.15006) reaches 56.2% on 691 task-and-model pairs, about 3 points above the average of 5 other harnesses, and 10.7 points more on GLM-5.3. MultiLoop (arXiv 2611.15754, already a Nov 13 term) improved 4.6% with only 10 examples, but most orchestration failures remained. Effectiveness 3/5, hype 2/5. Fit is medium: it confirms that the harness matters, but the gap is small and model-dependent, as in g-harness-evals on Nov 9. The harness has come up almost every day (Nov 5, 6, 8 and 9). Nov 15 update: the component worth trying immediately is Outcome Grounding. It blocks "I'm done" claims that have no evidence. The gain is especially large with GLM-5.3 (+10.7) and Kimi K3 (+7.9). There is no code link. The recommendation stays Watch.

## Sources

- [EvoX](https://arxiv.org/abs/2611.15006)
- [MultiLoop](https://arxiv.org/abs/2611.15754)
