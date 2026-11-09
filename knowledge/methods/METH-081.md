# METH-081: Weight-Space Programming (MIT CSAIL): a general model reads and edits raw network weights

## Summary

GPT-6 Astra takes a network's raw weights, explains what it does, and fixes or writes weights with no gradients or training; in Qwen3.5-0.8B it found and removed a direction in layers 15 and 19 that caused reasoning loops (0.016% of weights).

## Details

Critics (Neel Nanda, Haseeb Qureshi, Justin Angel) say it is mostly known interpretability techniques (direction ablation), not new 'x-ray vision'. Evidence: full logs published; Hugging Face rebuilt the edited model and re-ran evals: MATH-500 7.9% -> 48.1%, IFEval 21% -> 62.3%. Stated limits: no gain on Gemma 3 270M (which didn't loop); first attempts to detect a sycophantic model from weights alone failed; authors: 'editing removes an obstacle, it doesn't add capability'. 2,475 points on HN. Fit for AI products: low for now; relevant to future audit, unlearning and targeted fixes of small models. Recommendation: Watch.

## Sources

- [Weight-Space Programming (blog)](https://rikiyat.github.io/blog/weight-space-programming/)
- [Full logs](https://github.com/RikiyaT/lm_understand-logs)
