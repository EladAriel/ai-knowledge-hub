# METH-002: Decision models ('System One', typed decision models)

## Summary

What it is: the model receives a state and some defined questions: yes or no, a choice from a list or a score. It does not write text, but returns a probability for each possibility. You only pay for the input: $0.042 per million tokens on Jev and Decision-1, and $0.10 on OpenAI.

## Content

### 1. Decision models ("System One", typed decision models)
Sources: [Microsoft-Decision-1 (9.10)](https://commandline.microsoft.com/microsoft-decision-1-model-foundry/) · [TypeSafe Jev, System One docs](https://docs.typesafe.ai/concepts/system-one) · [OpenAI Decisions API (6.10)](https://developers.openai.com/api/docs/guides/decisions)

- **What is it:** The model receives a state and some defined questions: yes or no, a choice from a list or a score. It does not write text, but returns a probability for each possibility. You only pay for the input: $0.042 per million tokens on Jev and Decision-1, and $0.10 on OpenAI.
- **New or rebrand:** Mostly a rebrand of zero-shot classification with calibrated probabilities, such as classification by logprobs, NLI or cross-encoder. What's really new is a dedicated API without output tokens, several questions in one pass, and three major vendors adopting the same format in the same week.
- **Evidence:** The speed and accuracy data come from the providers themselves. Microsoft claims it's first in 36 benchmarks, but it can't be replicated. Decision-1 is Qwen3.5-9B with post-training. Jev has no paper and no weights. In an independent test, [TypedBench](https://arxiv.org/abs/2610.11392), the model is sensitive to formulation and systematically underconfident, and when errors have asymmetric costs its probabilities can be harmful.
- **Effectiveness** 4/5 | **Hype** 5/5
- **Fit:** High for routing, triage, filtering segments in RAG and judging traces. **low** effort.
- **Recommendation: Pilot** for routing and judging, with eval on your data. **No** as a security layer.

## Sources

- [Microsoft-Decision-1 (9.10)](https://commandline.microsoft.com/microsoft-decision-1-model-foundry/)
- [TypeSafe Jev, System One documents](https://docs.typesafe.ai/concepts/system-one)
- [OpenAI Decisions API (6.10)](https://developers.openai.com/api/docs/guides/decisions)
- [TypedBench](https://arxiv.org/abs/2610.11392)
