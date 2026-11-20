# METH-173: Can You Trust Your Finance Agent? Drift, diagnosis and auditable changes on one shipped agent

## Summary

The authors took the untuned reference agent from Vals Finance Agent Benchmark v2. Seven identical runs passed anywhere from 105 to 123 of 149 rubric criteria, and the cost varied by up to 17%. Score and bill are noisy even with nothing changed. Effort: low (mostly discipline, not infra). arXiv 2611.17939, Nov 13.

## Details

Failure ownership: 20 failed traces were sorted by whose layer fixes them, using a taxonomy fixed in advance. 13 belonged to instructions, 3 to tools, 4 to the model, 0 to data. Blind readers named the same fault as the LLM analyzer 94% of the time, about the same as their 93% agreement with each other.

Change control: an optimizer loop made one change per round and kept it only if it cleared a pre-set threshold. Optimizing for cost gave 0.34× cost on held-out questions (95% CI 0.22–0.58) with accuracy within noise. Optimizing for accuracy gave +14 points on dev questions but only +1.5 on held-out (CI −5.3 to +7.2), so that gain is not real. Limits: one agent and 9 test questions, so this is a case study.

Adopt for: Architects route each failure by owner layer (instructions / tools / model / data) and send it to that owner's queue. Product measures run-to-run noise (N identical runs) before announcing any improvement. Devs make one change per PR, and only promote it if the held-out delta is bigger than the noise band. See also EVAL-024.

## Sources

- [Can You Trust Your Finance Agent?](https://arxiv.org/abs/2611.17939)
