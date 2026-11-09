# EVAL-014: Eval: unanswerable-question test (Correct Abstention Rate)

## Summary

Mix in questions the docs can't answer and check the system declines; track CAR next to accuracy.

## Details

DeclineCraft (27 models): multi-step RAG lowered correct declines in 30/40 setups; query rewriting + reranking lowered them for all 12 models with almost no accuracy gain. Steps: 30-50 unanswerable questions (post-index topics, nonexistent projects, docs the user can't see); 10-20 old-vs-new conflict cases; make them 20-30% of the golden set; score declined/correct/wrong via regex or small judge; fail CI if CAR drops >5 points after a retrieval change.

## Content

## Simple eval technique: the unanswerable-question test

**What it is:** you mix in questions your documents can't answer, and check that the system says "I don't know" instead of guessing. The headline score is the Correct Abstention Rate (CAR), the share of unanswerable questions it correctly declines. It's based on [DeclineCraft](https://arxiv.org/abs/2610.28340) (Oct 20).

**Why now:** DeclineCraft tested 27 models. Multi-step RAG lowered correct declines in 30 of 40 setups. Adding query rewriting and reranking lowered them for all 12 models tested, with almost no gain in accuracy. In other words, the "better" pipeline guesses more.

**Steps (under a day):**
1. Write 30–50 questions your system can't answer. Good sources are topics added after your index was last built, a project that doesn't exist, and a doc the user isn't allowed to see.
2. Add 10–20 conflict cases where an old and a new version of a doc disagree, using [MMEnterprise-Bench](https://mlvlab.github.io/MMEnterprise-Bench/) as a template. The right answer is the newest version, or a decline.
3. Make these 20–30% of your golden question set.
4. Score each answer as declined, answered correctly, or answered wrongly, using a regex or a small LLM judge.
5. Track CAR next to accuracy, and fail CI if CAR drops more than 5 points after a retrieval change.

**What it catches:** confident made-up answers, extra guessing caused by reranking or agent loops, and answers taken from an old version of a doc. The "doc this user can't see" questions also catch permission leaks.

**Who runs it:** Product writes the "should say I don't know" cases, Devs wire it into CI, and Architects set the minimum CAR for production.

## Sources

- [DeclineCraft](https://arxiv.org/abs/2610.28340)
- [MMEnterprise-Bench](https://mlvlab.github.io/MMEnterprise-Bench/)