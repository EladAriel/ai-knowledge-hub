# EVAL-021: Decision models as cheap hallucination judges

## Summary

Judges that return only a label + probability matched a large text judge on context contradictions and came within 3 points on factual errors.

## Details

Trailed by 4-8 points on logic and instruction-following. Use in a confidence cascade: cheap judge first, bigger judge when unsure.

## Content

**2. [Decision models as judges for hallucination detection](https://arxiv.org/abs/2610.37229)**
- **The idea:** a decision model is a judge that returns only a label and a probability, with no free text.
- **How it did:** the best one matched a large text-generating judge on answers that contradict their context, and came within 3 points on factual errors. It trailed by 4–8 points on logic and instruction-follow... the host app, not the model, to approve any extra tool calls.
- Adopt for:
  - *Architects:* the host decides which tool calls each task is allowed, not the model.
  - *Product:* a successful task isn't the same as a safe one, so add a leak metric to the release checklist.
  - *Devs:* alert on any tool call that comes after the final answer, or that isn't on the task's allowed list.

## Sources

- [Decision models as judges](https://arxiv.org/abs/2610.37229)