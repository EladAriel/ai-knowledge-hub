# METH-103: GraphRail: checking each reasoning step without an LLM judge

## Summary

Turns the question, retrieved evidence and model reasoning into fact triples; deterministic code matches the three. Flags missing/unused/unresolved/grounded/unsupported/conflict per answer part—no reference answer, no LLM judge.

## Details

Results: offline often catches >90% of problems (better than LLM checkers); feeding feedback back raised Search-R1 exact-match on 2Wiki from 38.8 to 46.4; even a 0.5B extractor beat larger LLM judges. Costs/limits: ~1.5k extra tokens per check; helped less with ReAct-style agents. Effort: medium to high. Adopt for: Architects add an evidence check before the final answer; Product score whether every step was backed by evidence; Devs start with a small extractor plus deterministic matcher.

## Sources

- [GraphRail (arXiv)](https://arxiv.org/abs/2611.06662)
