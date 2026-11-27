# METH-202: DM-PRM: a decision model as a step judge (Pilot)

## Summary

When you train agents with RL there is one score at the end of each run, and no way to know which step helped. When every run fails, the agent learns nothing. DM-PRM asks a decision model (a yes/no question with a probability) one question about each step: "did this make progress?" No labels, training or critic are needed. The authors report a gain of more than 20 points on ALFWorld and 10 on WebShop, on a 1.5B model. The same idea can be used without training, to rank steps in traces in evals. These are the authors' results only, and no code was seen. Decision models have come up in this digest for the ninth time (October 10, November 7, 10, 12 and 14, then AnyS1 on November 19 and LoopRoute on November 20). Recommendation: Pilot, medium effort, and only if you train agents. arXiv 2611.27068.

## Details

From the Nov 23 methods digest. This is a new row, not a merge into METH-186 or METH-194: a step judge, not a router.

## Sources

- [DM-PRM](https://arxiv.org/abs/2611.27068)
