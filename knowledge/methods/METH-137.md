# METH-137: SELD: compression that quietly drops the evidence

## Summary

Compressing the context can delete the key evidence while the answer stays the same. The answer then has nothing behind it, which is risky when other agents reuse that context. SELD spots this with no training or labels: it compares how the model ranks the answers it didn't pick, before and after compression.

## Details

Results: it caught the cut that removed evidence 83% of the time, versus 70% for the best existing method. Effort: medium. Adopt for: Architects—treat compressed context as its own derived output with its own quality check; Product—only accept compression savings once you've shown the evidence survives; Devs—in CI, check that cited chunks survive compression, not just that answers stay the same. arXiv 2611.12903.

## Sources

- [SELD (arXiv)](https://arxiv.org/abs/2611.12903)
