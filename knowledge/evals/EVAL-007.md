# EVAL-007: Eval: citation correctness (ALCE recall/precision)

## Summary

For every claim, check the cited chunks support it: citation recall and citation precision.

## Details

1) Structured output [{claim, chunk_ids}]. 2) Log cited chunk text. 3) Code checks first: cited IDs were retrieved, user may see them, flag uncited claims. 4) LLM judge yes/no per claim ('fully supports?') and per citation ('needed?'). 5) Hand-label 30-50 claims to validate the judge. 6) Run on the golden set in CI; fail when citation recall drops below baseline. Next level: remove/alter the cited chunk and see if the answer changes (Wallat et al.: up to 57% of citations fail = post-rationalization).

## Content

## Simple eval technique: citation correctness

**What it is:** for every sentence in an answer, you check whether the chunks it cites actually support it. That gives you two numbers. Citation recall is the share of claims fully supported by their citations, and citation precision is the share of citations that were actually needed. This is the ALCE method ([Gao et al.](https://arxiv.org/abs/2305.14627)).

**How to start in under a day:**
1. Make the answer model return structured output, `[{claim, chunk_ids}]`, so every sentence carries its citations.
2. Log the text of every cited chunk with each answer.
3. Run plain code checks first, with no LLM. Every cited ID must have actually been retrieved, and the user must be allowed to see every cited doc, which ties back to yesterday's permissions work. Flag any claim with no citation.
4. Have an LLM judge answer one yes/no question per claim: "Does this cited text fully support this claim?" Then ask, for each citation, whether it was needed.
5. Label 30 to 50 claims by hand and check that the judge agrees with you before you trust it.
6. Run it on yesterday's golden question set in CI, and fail the build when citation recall drops below your baseline.

**Next level:** test whether the model really used its citations. Remove or change the cited chunk and see if the answer changes. If it doesn't, the citation was added after the answer was already decided. [Wallat et al.](https://arxiv.org/abs/2412.18004) found up to 57% of citations failed this test.

**What it catches:** made-up support, citations to the wrong document, answers stitched together from pieces of chunks, citations to docs the user can't see, and a model answering from its own memory while looking grounded.

**Who runs it:**
- *Devs* build it into CI.
- *Product* sets the minimum score and reviews failing claims each week, since that's where users lose trust.
- *Architects* define the citation format, with stable chunk IDs and source and permission fields on every chunk.

## Sources

- [ALCE (Gao et al.)](https://arxiv.org/abs/2305.14627)
- [Wallat et al.](https://arxiv.org/abs/2412.18004)