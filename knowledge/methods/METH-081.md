# METH-081: Weight-Space Programming (MIT CSAIL): a general model reads and edits raw network weights

## Summary

GPT-6 Astra takes a network's raw weights, explains what it does, and fixes or writes weights with no gradients or training; in Qwen3.5-0.8B it found and removed a direction in layers 15 and 19 that caused reasoning loops (0.016% of weights).

## Details

Critics (Neel Nanda, Haseeb Qureshi, Justin Angel) say it is mostly known interpretability techniques (direction ablation), not new 'x-ray vision'. Evidence: full logs published; Hugging Face rebuilt the edited model and re-ran evals: MATH-500 7.9% -> 48.1%, IFEval 21% -> 62.3%. Stated limits: no gain on Gemma 3 270M (which didn't loop); first attempts to detect a sycophantic model  keeps it at Watch, seeing it as familiar interpretability techniques.

## Content

**1. [Weight-Space Programming (MIT CSAIL)](https://rikiyat.github.io/blog/weight-space-programming/)**
- **What it is:** The GPT-6 Astra model accepts raw grid weights. He understands from them what the network does, and fixes them or writes them from scratch, without gradients and without training. In Qwen3.5-0.8B he found an orientation in layers 15 and 19 that causes thought loops, and removed it. The change affected 0.016% of the weights.
- **Why new:** General model, without changes, makes interpretability and direct editing. Critics (Neel Nanda, ‏Haseeb Qureshi, ‏Justin Angel) claim that this is mainly an activation of known techniques, such as directional ablation, and not a new "x-ray vision".
- **Evidence:**
  - have [full logs](https://github.com/RikiyaT/lm_understand-logs), and Hugging Face restored the edited model and ran the re-evaluation.
  - In MATH-500 the score increased from 7.9% to 48.1%, and in IFEval from 21% to 62.3%.
  - The limitations are stated: in the Gemma 3 270M, which did not get stuck in the loops, there was no improvement, and attempts to detect flattery from the weights also failed.
  - The authors themselves write that "editing removes an obstacle, not adds ability".
  - In HN the post received 2,475 points.
- **Scores:** Effectiveness 3/5, Hype 5/5.
- **Compatibility:** Low at the moment. This is relevant to the future of audit, unlearning and targeted repair of small models. **high** effort.
- **Recommendation: Watch**

**New names and terms**
- **From yesterday:** Weight-Space Programming now has a [review by Matthew Honnibal](https://honnibal.dev/) (963 points on HN), who claims the post is misleading. [Simon Willison](https://simonwillison.net/) showed that Qwen 3.8 27B on a laptop also does some of this.

## Sources

- [Weight-Space Programming (blog)](https://rikiyat.github.io/blog/weight-space-programming/)
- [Full logs](https://github.com/RikiyaT/lm_understand-logs)
- [Honnibal critique](https://honnibal.dev/)
- [Simon Willison](https://simonwillison.net/)