# METH-025: INO: user corrections become retrievable knowledge nuggets

## Summary

Turn factual corrections into short KB entries, test against the unchanged RAG with paraphrases, rewrite until retrieved and cited.

## Details

110 held-out queries: retrieval 52.3% -> 77.3%, citation 41.3% -> 68.1% vs storing as-is; support tickets retrieval 35.1% -> 78.2%; nuggets surfaced in 1.4% of 1,400 random queries with no false positives; ~$0.31 per nugget. Limits: one retrieval setup, English, LLM-dependent. Devs: copy the loop (index, test, check citation, rewrite up to 3x), keep test queries as regression tests; 'correction' doc type with provenance and owner approval.

## Content

### [INO: user corrections become knowledge entries the system can actually find (Mosaic AI)](https://arxiv.org/abs/2605.25641)
- **What:** The system filters feedback for factual corrections and turns each one into a short "nugget" (a small knowledge-base entry). It tests the nugget against the unchanged production RAG stack using the trigger query plus fresh paraphrases. It rewrites the nugget until it is retrieved and cited. A new version (v2) was posted 19 Oct; v1 is from May.
- **Numbers vs baseline (nugget stored as-is):** On 110 real held-out queries, retrieval went from 52.3% to 77.3% and citation from 41.3% to 68.1%. On support tickets, retrieval went from 35.1% to 78.2%. Answers that applied the correction went from 52.2% to 73.4%. Nuggets showed up in only 1.4% of 1,400 random queries, with no false positives. Hiding nuggets from 20% of users cut thumbs-up by 11.44% (p=0.055, borderline). Cost was about $0.31 per nugget.
- **Why it matters:** Feedback becomes a reviewed, owned, removable artifact. Nothing is edited in the source docs or prompts. Stated limits: one retrieval architecture, English only, and dependence on an LLM.
- **Effort:** med
- **Adopt for:**
  - **Architects:** Add a "correction" document type with provenance (feedback ID, owner, product version). A knowledge owner must approve it before it is published.
  - **Product:** Treat thumbs-down with a comment as a work queue. Track time from correction to published fix.
  - **Devs:** Copy the loop: index the nugget, run probe queries, check it was retrieved and cited, and rewrite it at most 3 times. Keep the probes as regression tests.

## Sources

- [INO (Mosaic AI)](https://arxiv.org/abs/2605.25641)