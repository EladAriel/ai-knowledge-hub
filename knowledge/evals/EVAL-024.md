# EVAL-024: Eval: pass^k (repeat-run consistency)

## Summary

Run each golden question k times (e.g. 5) and count questions answered right on every run, not just once (idea from tau-bench). Since identical runs can differ widely (a Nov 18 finance-agent study saw 105 to 123 of 149 criteria pass across seven identical runs), measure this noise band before claiming any improvement.

## Details

1) Take 30-50 existing questions. 2) Run each 5 times with normal settings. 3) Grade pass/fail with your existing check. 4) Report pass@5 (right at least once) and pass^5 (right every time). 5) List questions in the gap and find where they go wrong: retrieval order, chunks scoring the same, or answer step. Catches unstable retrieval, reranker tie-breaking, answers that change run to run, demos that worked once. Devs run in CI; Product sets threshold (e.g. pass^5 >= 80% on top use cases); Architects review the gap list. Effort: under a day.

Applied to an agent harness (Nov 1): before any harness change, run each fixed task k times and count success only if it passed every run; this gives a yardstick for whether a harness change really helped, and pairs naturally with a small eval of 5-10 fixed tasks. Effort low-medium. Implementation sketch (Nov 2): add a `--k` option to the harness's eval runner; each task runs k times on a fresh fixture copy with a shared run group; a report command for that run group prints passes/k per task plus total pass@1 and pass^k; a deliberately flaky task must show pass@1 > pass^k; default k=1 so cost doesn't jump.

Noise band (Nov 18, from "Can You Trust Your Finance Agent?", arXiv 2611.17939; see METH-173): the untuned reference agent from Vals Finance Agent Benchmark v2 passed anywhere from 105 to 123 of 149 rubric criteria across seven identical runs, and cost varied by up to 17%. Treat that spread across N identical runs as the noise band: a change smaller than the band is not an improvement, so only promote a change if its held-out gain is bigger than the noise.

## Content

### Simple eval technique: pass^k, or repeat-run consistency

**What it is:** run each golden question k times (say 5), then count the questions answered right on every run, not just once. The idea comes from [tau-bench](https://arxiv.org/abs/2406.12045).

**Steps (under a day):**
1. Take 30–50 questions you already have.
2. Run each one 5 times with your normal settings.
3. Grade each answer pass or fail with your existing check.
4. Report two numbers: right at least once (pass@5) and right every time (pass^5).
5. List the questions in the gap between the two, and find where they go wrong: retrieval order, chunks scoring the same, or the answer step.

**What it catches:** unstable retrieval, rerankers breaking ties differently each run, answers that change from run to run, and demos that only worked once.

**Who runs it:** Devs run it in CI. Product sets the threshold, for example pass^5 of at least 80% on the top use cases. Architects review the gap list for design causes.

### pass^k before changing a harness

Run each fixed task k times, and count it as a success only if it passed in all runs, not in just one of them. This gives a scale for deciding whether a change to the harness really improved anything, and it connects to an eval of 5–10 fixed tasks. Low-medium effort. Source: [tau-bench](https://arxiv.org/abs/2406.12045).

## Sources

- [tau-bench](https://arxiv.org/abs/2406.12045)
- [Can You Trust Your Finance Agent? (noise band)](https://arxiv.org/abs/2611.17939)
