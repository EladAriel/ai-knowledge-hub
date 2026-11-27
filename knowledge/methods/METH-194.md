# METH-194: LoopRoute: the large model steps in only when the agent is stuck in a loop (Pilot)

## Summary

A small decision model (Jev) is cheap and fast, but sometimes it repeats the same action without making progress. LoopRoute watches for the same state and the same action coming back. Then the large model gives a short piece of advice and returns control to the small model. No training or calibration is needed. The authors report gains of 21%, 60% and 30% versus Jev alone on three benchmarks, with few calls to the large model. Decision models have come up in this digest for the eighth time. What is new is a cheaper trigger than the confidence threshold in AnyS1 (METH-186). Recommendation: Pilot. Effort: low. arXiv 2611.25363.

## Details

From the Nov 20 methods digest. This is a new row, not a merge into METH-186.

## Sources

- [LoopRoute](https://arxiv.org/abs/2611.25363)
