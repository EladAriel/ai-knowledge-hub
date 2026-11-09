# METH-056: Simple harnesses beat SOP-driven agents (arXiv RCA study)

## Summary

On 90 microservice RCA cases, harnesses that don't script model calls hit 65-77% accuracy vs 16-53% for fixed-step SOP agents.

## Details

Fixed steps skip exactly the deciding evidence. Raising reasoning effort changed accuracy by a few points at most but up to 7x the time. Takeaway (agent): gates should check the output (tests, findings, diff, budget), not dictate the order of work; check whether feature-pipeline over-prescribes steps; default effort medium, not xhigh. Caveat: RCA, not coding.

## Content

The article s with SOP and fixed steps. The simple reached 65 to 77% accuracy, and the complex 16 to 53%. The reason they point to it is that the regular steps skip the very evidence that is decisive. Another finding: increasing the reasoning effort changed the accuracy by a few points at most, but doubled the time up to 7 times.

The conclusion for you: the gates should check the product (tests, findings, diff, budget) and not determine for the model in which order to work. You should also check if the feature-pipeline does not dictate too many steps, and the default for effort will be medium and not xhigh.

I put the harness eval and subagents token count in the budget into the 9:00 bid queue. The eval will probably come early, because it is what makes it possible to measure everything else.

## Sources

- [arXiv 2610.35767](https://arxiv.org/html/2610.35767v1)