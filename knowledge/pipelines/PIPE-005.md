# PIPE-005: Pipeline: agent and answer layer

## Summary

question + identity -> plan sub-queries -> hybrid search over a navigation layer -> fetch sources -> draft -> validate in code (exact quotes, schema, ACL) -> search again if evidence missing -> cite or decline and log a content gap.

## Details

Enforce the evidence contract in code (reject citations that aren't exact substrings). Let the agent search again after drafting. Answer only with the asker's access; run writes under the user's own connection. Count each source once (Memory Echo: 0.825 -> 0.920 accuracy in one setup). Pick path by latency: agent loop (~90 s) for review-heavy workflows, fixed pipeline (~8 s) for chat. Product routes 'no evidence' answers to content owners as tickets.

## Content

## Pipeline pattern of the day: the agent and answer layer

question + asker's identity -> plan sub-queries -> hybrid search over a navigation layer -> fetch the source docs -> draft the answer -> validate in code (exact quotes, schema, ACL) -> search again if evidence is missing -> answer with citations, or decline and log a content gap

- **Enforce the evidence contract in code.** Reject any citation that isn't an exact substring of its source ([Airbnb](https://arxiv.org/abs/2610.14428)).
- **Let the agent search again after drafting.** Airbnb's production pipeline searched once before writing and couldn't fill gaps afterward.
- **Answer only with the asker's access, and run writes under the user's own connection** ([company-brain permissions](https://github.com/supermemoryai/company-brain/blob/main/docs/guide/permissions.md)).
- **Count each source once.** Keep one record per source family, prefer corrected and authoritative records, and give old claims no extra weight for being repeated. In [Memory Echo](https://arxiv.org/abs/2610.17763) this raised accuracy from 0.825 to 0.920 in one setup.
- **Pick the path by latency.** Use an agent loop (about 90 s) for review-heavy workflows and a fast fixed pipeline (about 8 s) for chat.
- **Who owns it:**
  - *Architects* own the output contract and where the validator sits, plus the rule that permissions are checked outside the model.
  - *Product* decides which workflows can take slow, thorough answers, and sends "no evidence" answers to content owners as tickets.
  - *Devs* ship the manual-plus-scripts skill template and put the validator in CI.

## Sources

- [Airbnb](https://arxiv.org/abs/2610.14428)
- [Memory Echo](https://arxiv.org/abs/2610.17763)
- [company-brain permissions](https://github.com/supermemoryai/company-brain/blob/main/docs/guide/permissions.md)