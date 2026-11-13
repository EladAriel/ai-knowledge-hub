# METH-117: Strands Decider replaces Sonnet 4.6 for ticket tagging at Amazon

## Summary

Amazon replaced Sonnet 4.6, which tagged internal tickets into 20 categories, with the Strands Decider E4B decision model. The model does not generate text; it returns a probability per option and a confidence score, and runs on SageMaker.

## Details

What's new: a large-scale production case with a staged rollout, after the decision-model theme on Oct 10, Nov 7, and Flide (Nov 9). AppConfig switch with three modes—BEDROCK, DUAL and DECIDER; in DUAL both models run in parallel and are compared. Context window is 4,096 tokens, so every label description was rewritten as a one- or two-sentence criterion. Vendor-reported: 897ms vs 4,215ms, 2,010 tokens/ticket vs 6,724, and about 98% lower cost; they also say E4B beat Sonnet on a held-out set—all self-reported, no open data. HN (item 50436640, 155 points) noted Haiku or BERT might give similar savings. An independent AWS Builder Center benchmark found it excellent at judging task difficulty (AUC 1.00 vs 0.88) but 11–13 seconds per decision on CPU. Scores: effectiveness 4/5, hype 3/5. Fit: high for any high-volume classify/route/filter product. Effort: medium (GPU and rewritten labels). Recommendation: Pilot. Adopt the DUAL parallel run already on any model swap.

## Sources

- [Strands Decider (Amazon)](https://strandsagents.com/blog/amazon-saves-millions-replacing-sonnet-with-strands-decider/)
- [HN 50436640](https://news.ycombinator.com/item?id=50436640)
- [AWS Builder Center benchmark](https://builder.aws.com/content/3KRx3G8JMf1G06ZFu2dDEdE2DLw/benchmarking-strands-decider-llm-classifiers-and-bedrock-routing-for-model-routing)
