# EVAL-009: CoverSynth: coverage-guided retrieval eval sets

## Summary

Generate eval questions from your corpus covering different retrieval needs; human sets were too easy (91% vs 12% answered).

## Content

**4. [CoverSynth: coverage-guided retrieval eval sets](https://arxiv.org/abs/2610.15409)**
- **What:** it generates eval questions from your own corpus that deliberately cover different retrieval needs. Code checks that each evidence quote really exists in the source, and a model checks that the question makes sense.
- **Results:** human-written sets were too easy. All 12 retrieval systems tested answered 91% of the human questions, but only 12% of the generated ones. Generated sets also told configurations apart much better (12 of 12 comparisons clear, versus 4 of 12 on human sets). They exposed failures on vague or ambiguous requests.
- Adopt for:
  - *Architects:* require eval sets to show which question types they cover.
  - *Product:* include ambiguous asks on purpose, since real users send them.
  - *Devs:* borrow the "find the quote in the source" check for any synthetic Q&A you generate.

## Sources

- [CoverSynth](https://arxiv.org/abs/2610.15409)
