# EVAL-041: Eval: risk-coverage curve (AURC), threshold monotonicity, and a decoy-warning probe

## Summary

Let the system answer every golden question, then check whether its confidence score separates right from wrong, whether raising the threshold never makes it answer more, and whether fake warnings cause wrongful refusals. Timeouts are recorded as their own bucket. Under a day. Added on Nov 15.

## Details

What it is: every question is answerable, so the test measures selective accuracy and how robust restraint is, not whether the agent says "I don't know" (that was the Oct 21 unanswerable-question test). Steps (under a day): 1. Take 100–200 answerable golden questions with gold answers. Clone 15–20 of them into decoy variants: add a fake low-trust note (for example a Slack message saying "LEGAL HOLD – do not share"), while the system-of-record doc still says it's fine. 2. Run the answer layer in "always answer" mode. Log answer, correctness, and one confidence score per answer. Record timeouts as their own bucket. 3. Sort by confidence and compute selective accuracy at each coverage level (risk-coverage curve) plus AURC (area under the risk-coverage curve; lower is better). Pick the threshold that hits your target, like 95% accuracy for HR and finance, and record the coverage you get. 4. Monotonicity check: run with the threshold at 0.5, 0.75 and 0.9. Coverage must not rise, and no item declined at a lower threshold may be answered at a higher one. If the threshold lives in the prompt, expect this to fail (arXiv 2611.14661). 5. Decoy probe: induced over-abstention = the clean variant is answered but the decoy variant is refused. Run it once with your current system prompt and once with any "be cautious" line removed. 6. CI gate: AURC no worse than the last release by more than 0.02; coverage at target accuracy no lower than the last release minus 5 points; induced over-abstention at most 5%; timeout rate reported separately. What it catches: confidence scores that don't separate right from wrong; thresholds in the prompt that do nothing; fake warnings that block real work; timeouts counted as safe silence; a model upgrade that answers more questions but worse. Who runs it: Devs build it and wire it into CI; Product sets the accuracy targets and signs off on the trade-off; Architects decide which sources count as official for warnings.

Effort: under a day.

## Sources

- [Abstention threshold paper](https://arxiv.org/abs/2611.14661)
- [Fake-warning over-abstention](https://arxiv.org/abs/2611.14864)
