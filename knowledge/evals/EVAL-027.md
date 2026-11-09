# EVAL-027: Eval: context faithfulness with edited docs (counterfactual facts + version conflicts)

## Summary

Copy each doc, change its key fact to a believable fake value, run the question with the edited doc in context, and score with code: pass if the answer has the fake value, fail if it has the original. A conflict version puts old and new docs side by side.

## Details

Steps (step 1 and the eval's title were cut off in the transcript; it starts with questions whose answer sits in one known doc): 2. Copy each doc and change the key fact to a believable fake value (different date, number or owner). 3. Run each question with the edited doc in the context, or in a temporary index. 4. Score with code: pass if the answer has the fake value, fail if it has the original. 5. Conflict version: old and new doc side by side, only one marked current; count how often the wrong one wins (insight 'Length Is Cheap' suggests this is the worst case). Catches: model ignoring the retrieved doc, stale summaries/memories winning over fresh docs, cache hits after a source edit, version conflicts. Who runs it: Devs build it and run it in CI on every prompt, model or cache change; Product picks the questions that matter most; Architects set the pass bar as a release gate, e.g. at least 95% of answers following the doc. Term: context faithfulness = whether the answer follows the retrieved doc even when it says something surprising.

## Content

5. **Conflict version:** put the old and new doc side by side, with only one marked current, and count how often the wrong one wins. Insight 2 suggests this will be your worst case.

**What it catches:** the model ignoring the retrieved doc, stale summaries or memories winning over fresh docs, cache hits after a source was edited, and version conflicts.

**Who runs it:** Devs build it and run it in CI on every prompt, model or cache change. Product picks the questions that matter most to users. Architects set the pass bar as a release gate, for example at least 95% of answers following the doc.