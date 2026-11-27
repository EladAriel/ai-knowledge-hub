# METH-081: Weight-Space Programming (MIT CSAIL): a general model reads and edits raw network weights

## Summary

GPT-6 Astra takes a network's raw weights, explains what it does, and fixes or writes weights with no gradients or training; in Qwen3.5-0.8B it found and removed a direction in layers 15 and 19 that caused reasoning loops (0.016% of weights). Nov 21 follow-up: in "self-rewriting", an open 27B model rewrites its own weights by its own reasoning, with no gradients or training, and gets better on problems it never saw.

## Details

Critics (Neel Nanda, Haseeb Qureshi, Justin Angel) say it is mostly known interpretability techniques (direction ablation), not new 'x-ray vision'. Evidence: full logs published; Hugging Face rebuilt the edited model and re-ran evals: MATH-500 7.9% -> 48.1%, IFEval 21% -> 62.3%. Stated limits: no gain on Gemma 3 270M (which didn't loop); first attempts to detect a sycophantic model from weights alone failed; authors: 'editing removes an obstacle, it doesn't add capability'. 2,475 points on HN. Fit for AI products: low for now; relevant to future audit, unlearning and targeted fixes of small models. Recommendation: Watch.

Nov 4 follow-up: Matthew Honnibal published a critique (963 points on HN) arguing the post is misleading, and Simon Willison showed Qwen 3.8 27B on a laptop does part of it; the item stays at Watch, as familiar interpretability techniques.

Update (Nov 21–22): self-rewriting continues this line of work (merged here rather than added as a new item). Instead of a frontier model editing a much smaller one, an open 27B model is given its own weights, its graded answers and the ability to run itself; it diagnoses its own failure and rewrites the weights behind it. Nov 22 update: over 8 consecutive sessions its accuracy only rises, and it brings a damaged copy of itself back to over 80% of the original accuracy. Recommendation stays Watch.

## Content

### Weight-Space Programming (MIT CSAIL), Nov 3

- **What it is:** the GPT-6 Astra model takes a network's raw weights. From them it works out what the network does, and fixes them or writes them from scratch, with no gradients and no training. In Qwen3.5-0.8B it found a direction in layers 15 and 19 that causes reasoning loops, and removed it. The change touched 0.016% of the weights.
- **Why it is new:** a general model, with no modifications, does interpretability and direct editing. Critics (Neel Nanda, Haseeb Qureshi, Justin Angel) argue that this is mainly an application of known techniques, such as ablating a direction, and not a new "x-ray vision".
- **Evidence:**
  - There are [full logs](https://github.com/RikiyaT/lm_understand-logs), and Hugging Face rebuilt the edited model and re-ran the evaluation.
  - On MATH-500 the score rose from 7.9% to 48.1%, and on IFEval from 21% to 62.3%.
  - The limits are stated: on Gemma 3 270M, which did not get stuck in loops, there was no improvement, and attempts to detect sycophancy from the weights also failed.
  - The authors themselves write that "editing removes an obstacle, it doesn't add capability".
  - On HN the post received 2,475 points.
- **Scores:** effectiveness 3/5, hype 5/5.
- **Fit:** low for now. It is relevant to the future of audit, unlearning and targeted repair of small models. Effort: **high**.
- **Recommendation: Watch**

### New names and terms, Nov 4

- **Follow-up from the day before:** Weight-Space Programming now has a [critique by Matthew Honnibal](https://honnibal.dev/) (963 points on HN), who argues the post is misleading. [Simon Willison](https://simonwillison.net/) showed that Qwen 3.8 27B on a laptop also does part of this.

### Self-rewriting: language models can rewrite their own weights, Nov 21–22

- **What it is:** a model is normally trained once and frozen; improving it takes another training run, or a prompt, a harness or extra inference-time compute that is gone once the task ends. Self-rewriting is a third way: the model is its own optimizer. An open 27B model, given its weights, its graded answers and the ability to run itself, diagnoses its own failure and rewrites the weights behind it, with no gradients and no training.
- **Reported results (authors' numbers):** its own edit makes it 6.6 points more accurate on problems it never saw. It tests its edits on practice problems and submits only what works, and over eight consecutive sessions its accuracy only rises. It repairs a damaged copy of itself: the copy solves almost nothing, yet without retraining and without reading the original weights, the model brings it back to over 80% of the original accuracy on unseen image tasks. The ability emerges with scale: in one model family, the smaller models make no edit or break themselves, and only the largest improves and repairs itself.
- **Why it matters:** unlike test-time scaling, the gain is written into the weights, at no cost per answer; unlike training, it runs only forward passes, as serving does.
- **Recommendation:** still Watch. See the [paper](https://arxiv.org/abs/2611.21885) and the [project page](https://www.jiajunfan.com/projects/self-rewriting/).

## Sources

- [Weight-Space Programming (blog)](https://rikiyat.github.io/blog/weight-space-programming/)
- [Full logs](https://github.com/RikiyaT/lm_understand-logs)
- [Honnibal critique](https://honnibal.dev/)
- [Simon Willison](https://simonwillison.net/)
- [Self-rewriting: Language Models Can Rewrite Their Own Weights](https://arxiv.org/abs/2611.21885)
- [Self-rewriting project page](https://www.jiajunfan.com/projects/self-rewriting/)
