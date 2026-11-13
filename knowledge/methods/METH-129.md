# METH-129: VulnCheck on Glasswing: metrics the system reports about itself vs what maintainers confirm

## Summary

A 7-month recap: 442 CVEs attributed to Anthropic; 217 fixes out of 37,966 findings, and 1,670 duplicates. On curl, 19 of 34 reports were marked 'not a vulnerability,' while Anthropic states 94.2% accuracy.

## Details

Why it matters: this is not a technique but a lesson about evals. Accuracy the system reports about itself is not the same as accuracy measured by the people who receive the findings. And when discovery volume goes up, the triage work moves to maintainers. Evidence: the numbers were taken from Anthropic and curl records, and there is an open tracking repo; VulnCheck is a competing company with a stated position, so the analysis is not neutral; 392 points on HN. Scores: effectiveness 4/5 as a lesson, hype 2/5. Fit: high for any product that produces findings, alerts, or recommendations. Effort low: measure how many of the findings the end user actually accepts. Recommendation: Adopt as a lesson. The theme of self-reported metrics continues after MaxxBench (Nov 9).

## Sources

- [VulnCheck on Glasswing](https://www.vulncheck.com/blog/anthropic-glasswing-november-update)
