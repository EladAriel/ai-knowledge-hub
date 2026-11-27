# METH-203: Snoop: a browsing agent leaks information through the pages it chooses to visit (Adopt-check)

## Summary

Even if no sensitive text goes out, the order of pages and searches a browsing agent makes can reveal the user's question and profile. The attack reconstructs the question topic at F1 0.89 and the profile at 0.80. Four existing defenses barely helped (less than 0.03). The authors' defense, SOR, pulls resources under a fixed budget and chooses among them locally, and it drops leakage to 0.39 with no extra LLM calls. This is a new vector that a content check does not catch, and it applies to any company assistant that browses with private context. Agent security has come up in a run (November 13, 20 and 22). Recommendation: Adopt-check, meaning add this to the threat model. Effort: low. arXiv 2611.27046.

## Details

From the Nov 23 methods digest.

## Sources

- [Snoop](https://arxiv.org/abs/2611.27046)
