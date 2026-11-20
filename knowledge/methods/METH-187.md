# METH-187: New terms (Nov 19, methods): Timeout Cascades, token heat, UDC, TRACE-MAS

## Summary

One-line mentions from the Nov 19 methods digest (no full evaluations).

## Details

Timeout Cascades: try a small model first, and move to a large one only after a timeout or a failure. The authors report 16% less GPU time on SWE-bench ([arXiv 2611.24324](https://arxiv.org/abs/2611.24324)).

Token heat: according to [arXiv 2611.23375](https://arxiv.org/abs/2611.23375), about 80% of the tokens in a successful coding-agent run do not advance the change.

UDC (Underspecified Decision Completion): a model that turns a question into a data query quietly fills in assumptions instead of asking. The hard part is noticing what it should have asked.

TRACE-MAS: a tool that finds the root of a failure in interactions between agents. The authors report 60% more accurate localization ([arXiv 2611.23362](https://arxiv.org/abs/2611.23362)).

Filtered and therefore not added: model launches (Gemini 4 Neon and seven Microsoft models), because they are products, not methods; and a KPMG story that reached Hacker News, because it was a press article without a checked primary source.

## Sources

- [Timeout Cascades](https://arxiv.org/abs/2611.24324)
- [Token heat](https://arxiv.org/abs/2611.23375)
- [TRACE-MAS](https://arxiv.org/abs/2611.23362)
