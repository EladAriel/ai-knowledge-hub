# METH-196: Improve the harness instead of training the model (Pilot)

## Summary

Adapting an agent to a domain by training (RL or SFT) is expensive, and hard to roll back. This paper automatically improves the prompt, the tool schemas and the skills library with GEPA, without changing the model. You get a harness adapter per domain, with no GPU. It was tested on SWE-bench, OfficeBench and Terminal-Bench. The authors report that this reaches most of the gain of training at a fraction of the cost, and that combining both approaches is best. One product can then hold an adapter per customer or domain. GEPA and prompt improvement have come up here before (October 10, 15 and 30, November 6 and 8). What is new is the direct comparison to training. Recommendation: Pilot. Effort: medium. arXiv 2611.25380.

## Details

From the Nov 21 methods digest, after the same paper was named as a term on Nov 20.

Related terms from the Nov 21 digest: a harness adapter is a prompt, tools and skills bundle that has been optimized for a domain and can be loaded when needed.

## Sources

- [Improve the harness instead of training the model](https://arxiv.org/abs/2611.25380)
