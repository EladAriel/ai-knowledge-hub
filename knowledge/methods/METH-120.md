# METH-120: Prompt-injection filters fail on legal contracts (high false-positive rates)

## Summary

A measurement of 11 open injection filters on two contract corpora. At document level, the false-positive rate reached 92.39%. No filter was better across all metrics than five simple regexes.

## Details

What's new: the authors present this as the first public measurement of such false positives on legal documents. Recommendation: Adopt as a test. Run a false-positive check on your own documents. Connects to the Hightouch calibrated cascade from Nov 7. arXiv 2611.08834.

## Sources

- [injection filters on contracts (arXiv)](https://arxiv.org/abs/2611.08834)
