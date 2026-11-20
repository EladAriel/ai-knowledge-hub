# PIPE-032: Pipeline: decide before you speak (already handled, threshold in code, verify before declining, cite-check)

## Summary

question or watched thread -> search for evidence within a fixed time and tool budget -> check against the system that owns the data: is this already handled, and is there enough evidence -> code decides whether to answer, ask, stay quiet or hand off -> draft with a citation per claim -> citation check, fixing by edits rather than a rewrite -> deliver to the right place (thread, DM or channel) -> reviewers give feedback, grouped by job type

## Details

Make "is this already handled?" its own step, and count false alarms separately. Unneeded messages look fine, so only a separate count catches them (Deepnote). Cap the search and force a decision. Log a timeout as its own outcome, because otherwise it gets counted as correct silence. Apply the decline threshold in code, on a calibrated confidence score, and recalibrate for each domain (threshold paper, arXiv 2611.14661). Only decline on evidence from an official source. "Be cautious" prompts made agents obey fake warnings (fake-warning paper, arXiv 2611.14864). A citation doesn't prove where an answer came from. Keep a citation check before shipping, and pull high-stakes values from the system that owns them (Cited but Unused, arXiv 2611.17161). Owners: Architects own the list of outcomes, where the threshold lives, which sources to trust most (the official system beats a ticket, and a ticket beats Slack), and the timeout rule, and publish all of this as a contract the UI and evals both read; Product sets target accuracy per risk area, decides when and to whom the agent hands off, and runs the review queue by job type; Devs write the decision as one plain function, decide(score, authority, budget_state) -> outcome, keep the citation check as its own step, and gate CI on EVAL-041. Added on Nov 15 (answer layer, fourth time on it).

## Sources

- [Deepnote Agent Initiative Benchmark](https://deepnote.com/research/benchmark)
- [Abstention threshold paper](https://arxiv.org/abs/2611.14661)
- [Fake-warning over-abstention](https://arxiv.org/abs/2611.14864)
- [Cited but Unused](https://arxiv.org/abs/2611.17161)
