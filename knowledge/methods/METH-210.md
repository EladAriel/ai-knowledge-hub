# METH-210: How an agent should see a screen (Adopt-check)

## Summary

A computer-use agent is given a screenshot, an accessibility tree, or both, and it is not clear which is better. Greptile ran 172 OSWorld tasks on 7 models. On weak models, the tree plus clicking by an element ID added 9 to 37 points. On the strong models (GPT-6.1 Sol, 83.8%) there was no difference. Their hybrid: always a screenshot, an ID when there is one, and coordinates for a canvas or for games. Why it matters: this has a direct cost effect, because a cheap model with a tree and IDs closes the gap. This is a company experiment, but with a full method and full numbers. Recommendation: Adopt-check. Effort: low.

## Details

From the Nov 24 methods digest.

## Sources

- [Greptile: how an agent should see a screen](https://www.greptile.com/blog/trex-computer-use)
