# EVAL-004: Eval: golden question set + retrieval recall@k (with negative ACL cases)

## Summary

Fixed real questions labeled with gold doc IDs; measure recall@5/@10, MRR and leak count per user in CI.

## Details

1) 50-100 real questions from Slack/tickets/search logs. 2) Gold doc IDs, expert spot-check ~20%. 3) 10-20 negative ACL cases (user, question, forbidden doc). 4) golden.jsonl {q,user,gold_ids,forbidden_ids}. 5) Script runs retriever as each user: recall@5/@10, MRR, leaks. 6) CI on every chunking/embedding/reranking/connector change; fail on >~3 pt recall drop or any leak. Catches chunking/embedding regressions, dead connectors, reranker changes, leaks; not answer quality.

## Content

## Simple eval technique: golden question set + retrieval recall@k

- **What:** a fixed list of real questions, each labeled with the doc or chunk IDs that contain the answer. **Recall@k** is the share of questions where at least one correct ID shows up in the top k results (or the share of all correct IDs found). It tests retrieval only, with no LLM grading.
- **Steps (under a day):**
  1. Collect 50–100 real questions from Slack, tickets, or search logs, across your main sources.
  2. For each, write down the gold doc ID(s). Have a domain expert spot-check about 20%.
  3. Add 10–20 **negative ACL cases**: (user, question, a doc that user must NOT see). Glean's advice: "test the negative case".
  4. Store everything as `golden.jsonl` with `{q, user, gold_ids, forbidden_ids}`.
  5. Write a script that runs the retriever as each user and computes recall@5/@10, MRR (how high the first correct hit ranks), and leak count (forbidden IDs returned).
  6. Run it in CI on every change to chunking, embeddings, reranking, or connectors. Fail on a recall drop of more than ~3 points or any leak.
- **What it catches:** chunking or embedding regressions, a connector that silently stopped syncing, reranker or threshold changes that drop good chunks, and permission leaks. It does not catch bad answer writing. For that, add answer grading later.
- **Who runs it:** Product owns the question list and target scores. Devs build the script and the CI gate. Architects own the negative ACL cases and review leaks.