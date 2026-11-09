# EVAL-014: Eval: unanswerable-question test (Correct Abstention Rate)

## Summary

Mix in questions the docs can't answer and check the system declines; track CAR next to accuracy.

## Details

DeclineCraft (27 models): multi-step RAG lowered correct declines in 30/40 setups; query rewriting + reranking lowered them for all 12 models with almost no accuracy gain. ….

## Sources

- [DeclineCraft](https://arxiv.org/abs/2610.28340)
