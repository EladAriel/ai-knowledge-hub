# METH-163: Perplexity Decider v1.3 and Flash v1.3: a fourth decision-model vendor, with span extraction

## Summary

Decision models that return probabilities instead of text: yes or no, multiple choice, or a score. The large model is built on Qwen3.8-27B, and a 4B Flash version was distilled from it. The new capability in this version is Locate, which extracts text spans word for word with character offsets and a confidence score, for uses such as NER, PII and extraction questions. Recommendation: Pilot.

## Details

The category already exists (Jev, Decisions API). What's new is span extraction inside the decision model, and an attention change in which each question sees only the context and itself, so answers don't affect one another. Evidence, all reported by Perplexity: 91.6% on average across 63 classification tasks, and a 0.27% answer flip rate. According to MarkTechPost, Locate is the weakest of the capabilities (69.0), and Flash lags Jev 1.14 in finance, programming and law. There are weights on Hugging Face, but while MarkTechPost reports an Apache 2.0 license, the HF card says the repo is private and needs an access token. 123 points on HN. Effectiveness 4/5, hype 2/5. Fit is high for routing, moderation, LLM-as-judge, reranking and filtering agent logs. Effort is low through the API or OpenRouter (posts on X said free until Nov 19), medium to self-host (about 49 GB GPU). Decision models came up almost every day this week: Oct 10, Nov 7, Nov 9 (Flide), Nov 10 (Strands), Nov 12 (Gemini) and Nov 13 (Actor/Judge). Perplexity is already the fourth vendor.

## Sources

- [Perplexity Decider v1.3](https://www.perplexity.ai/hub/blog/perplexity-decider)
