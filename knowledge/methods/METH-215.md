# METH-215: When an agent "fixes" an error and causes harm (Adopt-check)

## Summary

An agent runs a block of code with several write actions, the block fails in the middle, and the agent rewrites it and runs it again. On AppWorld, across 10 models, 24.6% of these fixes caused damage that was still there at the end of the run: duplicates, deleted data, or an order for the wrong product. A rule that looks for repeated calls catches only 41% of the damage. Idempotency keys the model itself mints do not help, because it invents a new identifier for the same action. Why it matters: any product where an agent writes to live systems (CRM, orders, tickets) is exposed to this. It continues the Nov 14 finding that "the world still holds the error" (METH-164). The data and scripts are open. Recommendation: Adopt-check. Effort: low to medium. Next step: check in your product what happens after a partial run: build idempotency keys from the content of the call, not from the model, and keep a journal of what was already written.

## Details

From the Nov 25 methods digest.

## Sources

- [When an agent fix causes harm](https://arxiv.org/abs/2611.31554)
