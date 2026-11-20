# METH-186: AnyS1: one small model for every decision point (Pilot)

## Summary

The agent calls a large model at every step, even when it only needs to choose among a few known options. AnyS1 extracts decision points from more than 1,000 public Skills and trains one small 4B model that makes the choice in a single call. When its confidence is below a calibrated threshold, the decision goes to the large model. The authors report 75–91% cost savings with no loss of reliability, on 3 benchmarks the model did not see in training. These are the authors' results only; no independent reproduction was reported. Recommendation: Pilot. Effort: medium. arXiv 2611.23751; code: middle-chunjie/AnyS1.

## Details

Noted on Nov 19. Why it matters: this is the seventh time a decision-model or model-router theme has come up (Oct 10, Nov 7, 10, 12, 13 and 14). What is new is that there is open-source code.

Related: METH-117 (Strands Decider), METH-139 (Gemini Decisions API), METH-163 (Perplexity Decider). This is a separate item, not a duplicate: a trained 4B router over extracted decision points, with a repo, not another vendor Decider.

## Sources

- [AnyS1](https://arxiv.org/abs/2611.23751)
- [middle-chunjie/AnyS1](https://github.com/middle-chunjie/AnyS1)
