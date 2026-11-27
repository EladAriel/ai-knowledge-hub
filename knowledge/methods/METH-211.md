# METH-211: FrameCheck: the numbers are right, the story is made up (Pilot)

## Summary

A report a model writes can show every number correctly, and still add reasons and judgments that were not in the input. The authors say that trying to fix this in the prompt actually made the problem larger. The fix is a layer between the model and the human reviewer: professional examples of a similar-size change, a mark on judgments and reasons that have no source, and removal by rules with no further model call. It was tested on 17 models and 3 million drafts. Why it matters: this is relevant to any product that produces reports. Checking that the numbers are right is not enough; you also have to check the narrative. Recommendation: Pilot. Effort: low to medium. arXiv 2611.26968; code: seunghan96/framecheck.

## Details

From the Nov 24 methods digest, after the same work was named as a term on Nov 23 (METH-205).

## Sources

- [FrameCheck](https://arxiv.org/abs/2611.26968)
- [seunghan96/framecheck](https://github.com/seunghan96/framecheck)
