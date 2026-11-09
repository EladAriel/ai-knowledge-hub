# EVAL-027: Eval: context faithfulness with edited docs (counterfactual facts + version conflicts)

## Summary

Copy each doc, change its key fact to a believable fake value, run the question with the edited doc in context, and score with code: pass if the answer has the fake value, fail if it has the original. A conflict version puts old and new docs side by side.

## Details

Steps (step 1 and the eval's title were cut off in the transcript; it starts with questions whose answer sits in one known doc): 2. Copy each doc and change the key fact to a believable fake value (different date, number or owner). 3. Run each question with the edited doc in the context, or in a temporary index. 4. Score with code: pass if the answer has the fake value, fail if it has the original.

## Sources

- (no public source link recorded)
