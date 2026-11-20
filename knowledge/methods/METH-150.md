# METH-150: SwitchIR: embeddings can't tell which way a question points

## Summary

Same query words and same documents, but the direction flips, like cause versus effect or before versus after. Across 7 neural retrievers, scores fall from 0.986 (attribute words signal the answer) and 0.923 (explicit filters) to 0.015 when only the direction flips; on a more realistic set, 0.943, 0.679 and 0.084. Effort: low, since it's a test idea.

## Details

Why it matters (arXiv 2611.15417): "who reports to Dana" and "who does Dana report to" look almost the same to an embedding. So do "what depends on service X" and "what does X depend on." Limits: it's an academic benchmark. Fine-tuning helps somewhat, more so in bigger models. Adopt for: Architects send directional questions, like org charts, dependencies and approvals, to graph or SQL lookups instead of vectors; Product list the directional questions users really ask, and mark them as needing a structured answer; Devs add flipped question pairs to your golden questions, as in EVAL-040.

## Sources

- [SwitchIR](https://arxiv.org/abs/2611.15417)
