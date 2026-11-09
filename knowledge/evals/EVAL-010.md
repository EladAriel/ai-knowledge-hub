# EVAL-010: Eval: LLM-as-judge with yes/no rubric, calibrated before trust

## Summary

Two yes/no judges (resolves the task? / rebuildable from cited snippets?) from a different model family, majority of 3, checked against human labels.

## Details

1) 30-50 real questions with approved answers (thumbs-up history). 2) Judge A: resolves task with nothing misleading; Judge B: answer rebuildable .

## Content

## Simple eval technique: LLM-as-judge with a yes/no rubric, checked before you trust it

**What it is:** a second model grades answers with a yes/no rubric. Before it gates anything, you check it against human labels.

**Steps (under a day):**
1. Collect 30–50 real questions with approved answers. You can reuse thumbs-up history, as Airbnb did.
2. Write two yes/no judges instead of 1–10 scores.
   - Judge A asks whether the answer resolves the task with nothing misleading.
   - Judge B asks whether someone could rebuild the answer from the cited snippets alone.
   - Have each judge list its checks, then end with `VERDICT accept/reject`.
3. Use a judge from a different model family than the one writing the answers. Run it 3 times and take the majority, since Airbnb saw about 15% disagreement between single runs.
4. Label about 50 outputs by hand and measure how often the judge agrees. In [AGO](https://arxiv.org/abs/2610.01218), a cheap judge was barely better than a coin flip at spotting bad answers (AUROC 0.603, where 0.5 is chance), versus 0.783 for a stronger one. Judge accuracy also varied by domain, from 0.62 to 0.88.
5. Wire both judges into CI as promptfoo `llm-rubric` assertions, and block merges on regressions.

**What it catches:** wrong procedures and claims the sources don't support. Comparing the two judges also tells you what to fix. If Judge A passes but Judge B fails, the answer is right but the sources can't prove it, so the corpus needs work. If Judge A fails, fix the agent.

**Who runs it:**
- *Product* writes the rubric and labels the calibration set.
- *Devs* wire it into CI.
- *Architects* own the judge model, its version, and the pass threshold.

## Sources

- [AGO](https://arxiv.org/abs/2610.01218)
- [promptfoo llm-rubric](https://www.promptfoo.dev/docs/configuration/expected-outputs/model-graded/llm-rubric/)