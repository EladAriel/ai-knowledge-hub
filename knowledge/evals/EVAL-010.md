# EVAL-010: Eval: LLM-as-judge with yes/no rubric, calibrated before trust

## Summary

Two yes/no judges (resolves the task? / rebuildable from cited snippets?) from a different model family, majority of 3, ….

## Details

1) 30-50 real questions with approved answers (thumbs-up history). 2) Judge A: resolves task with nothing misleading; Judge B: answer rebuildable from cited snippets; each lists checks then VERDICT accept/reject. ….

## Sources

- [AGO](https://arxiv.org/abs/2610.01218)
- [promptfoo llm-rubric](https://www.promptfoo.dev/docs/configuration/expected-outputs/model-graded/llm-rubric/)
