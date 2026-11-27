# METH-192: CompAct-Bench: how much an agent loses when its context is compressed (Adopt-check)

## Summary

On long runs a model summarizes the history to save context space, and no one measures how much the summary hurts the rest of the work. CompAct-Bench uses 200 tasks the agent had already solved. Mid-run, a model summarizes the history, and a fixed performer continues from that point. 12 leading models were tested as the summarizer. After compression, success falls to 56.7% on average, and even the best summarizer reaches only 68.5%. There are two failure types. When information is dropped, the agent repeats work it already did. When a guess is written in the summary as a fact, the agent stops too early. The topic has come up before (October 16, November 14); now it has a metric. Recommendation: Adopt-check, meaning run the same test on your own compression mechanism. Effort: low to medium. arXiv 2611.25673.

## Details

From the Nov 20 methods digest.

Related: METH-106 (SUMONE, a plug-in summarizer for long sessions).

## Sources

- [CompAct-Bench](https://arxiv.org/abs/2611.25673)
