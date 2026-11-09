# EVAL-024: Eval: pass^k (repeat-run consistency)

## Summary

Run each golden question k times (e.g. 5) and count questions answered right on every run, not just once (idea from tau-bench).

## Details

1) Take 30-50 existing questions. 2) Run each 5 times with normal settings. 3) Grade pass/fail with your existing check. 4) Report pass@5 (right at least once) and pass^5 (right every time). 5) List questions in the gap and find where they go wrong: retrieval order, chunks scoring the same, or answer step. Catches unstable retrieval, reranker tie-breaking, answers that change run to run, demos that worked once. Devs run in CI; Product sets threshold (e.g. pass^5 >= 80% on top use cases); Architects review the gap list. Harness (Nov 1): before any harness change, run each fixed task k times and count success only if it passed every run; gives a yardstick for whether a harness change really helped and connects to the queued 5-10 fixed-task eval. Effort low-medium. Harness task H-12 (Nov 2): add --k to harness-eval (H-11); each task runs k times on a fresh fixture copy with a shared run_group; 'harness-eval report \<run_group>' prints passes/k per task plus total pass@1 and pass^k; a deliberately flaky task must show pass@1 > pass^k; default k=1 so cost doesn't jump.

## Content

## Simple eval technique: pass^k, or repeat-run consistency

**What it is:** run each golden question k times (say 5), then count the questions answered correctly on every run, not just once. The idea comes from [tau-bench](https://arxiv.org/abs/2406.12045).

**Steps (under a day):**
1. Take 30-50 questions you already have.
2. Run each one 5 times with your normal settings.
3. Grade each answer pass or fail with your existing check.
4. Report two numbers: right at least once (pass@5) and right every time (pass^5).
5. List the questions in the gap between the two, and find where they go wrong: retrieval order, chunks scoring the same, or the answer step.

**What it catches:** unstable retrieval, rerankers breaking ties differently each run, answers that change from run to run, and demos that only worked once.

**Who runs it:** Devs run it in CI. Product sets the threshold, for example pass^5 of at least 80% on the top use cases. Architects review the gap list for design reasons.

1. **pass^k test before changing the harness.** Each fixed task is run k times, and is considered a success only if it passed in all runs, not in one of them. This gives a scale to decide if a change in harness really improved something, and connects to the eval of 5–10 fixed tasks already in the queue. Low-medium effort. Sources: [tau-bench](https://arxiv.org/abs/2406.12045) via company brain digest.

## Sources

- [tau-bench](https://arxiv.org/abs/2406.12045)