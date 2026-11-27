# METH-204: CodeReviewBench: measure review comments by what the user actually did (Adopt the method)

## Summary

Code-review benchmarks rely on outside labelers and on a fixed set of problems. CodeReviewBench counts a bot comment as useful if the developer applied it. The data is mined every day from GitHub events: more than 500,000 PRs and 18 tools, and the ranking matched hand labels. Why it matters: this is a pattern you can copy for any AI product, namely measure suggestions by a user's action, not by an LLM-judge. The idea of revealed preference is not new, but the application here is at a large scale. Eval completeness keeps coming up as a theme. Recommendation: Adopt-method. Effort: low. arXiv 2611.26942.

## Details

From the Nov 23 methods digest.

## Sources

- [CodeReviewBench](https://arxiv.org/abs/2611.26942)
