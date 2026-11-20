# EVAL-040: Eval: flipped-pair test plus recall by source

## Summary

Two small checks that an overall average hides: the same entities with the direction reversed, and recall at the agent's real k, broken down by data source and question type. Under a day. Added on Nov 14.

## Details

Steps: 1. From your own data, label the correct document for each side of flipped pairs, such as "who does Dana report to" and "who reports to Dana"; "what does billing-svc depend on" and "what depends on billing-svc"; "the policy that replaced X" and "the policy X replaced". 2. Run both sides through keyword search, vector search, hybrid search, and hybrid search plus the reranker. 3. Score pair accuracy: the share of pairs where both sides rank their own document above the other side's. Random guessing gets about 25%, and SwitchIR suggests embeddings will score low. 4. Tag each golden question with its source and question type. Then score recall in the top 16 for each question with `ir_measures.iter_calc`, and group the scores by tag. 5. In CI, fail the build if any source's recall or the pair accuracy drops past an agreed amount since the last release. What it catches: retrievers that ignore direction, rerankers that don't fix it, and quiet drops for one source that a good overall average hides. Who runs it: Devs build it and wire it into CI; Product writes the pairs from real user questions and sets the thresholds for each source; Architects use low pair accuracy as evidence to route those questions to a graph or SQL.

Effort: under a day.

## Sources

- [SwitchIR](https://arxiv.org/abs/2611.15417)
- [ir_measures](https://github.com/terrierteam/ir_measures)
