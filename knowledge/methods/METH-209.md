# METH-209: Claude Ship: agents that take a PR all the way to merge (Pilot)

## Summary

Agents write code quickly, but review, fixes and approvals still stall with people. Claude Ship uses three agents. Code Review checks findings against an agent that tries to refute them. PR Steward fixes CI, conflicts and comments, does not approve or merge, and after every push explains how to undo. Claude Approvals approves according to a policy file in the repo (a kind of smart CODEOWNERS), and the recommendation is to start in observe-only. Why it matters: the pattern itself — approval policy as a file, observe mode, and "how to undo" after every change — fits any product where an agent changes things. The numbers (2x merged PRs, 40% fewer reverts) are a vendor claim only. You can measure independently with CodeReviewBench (METH-204), which checks review tools by what developers actually fixed. The topic has come up before (November 10 and 12). Recommendation: Pilot. Effort: low.

## Details

From the Nov 24 methods digest. Two parts of this pattern are easy to copy into your own agent setup: an observe-then-enforce mode for new gates, and undo instructions after every agent push. Nov 25 update: Claude.dev published a practical shipping guide for the same product, with the `/code-review`, `/ship` and `/steward` commands, GA versus beta status, and a warning that `--fix` during a background review may not be caught by `/rewind` (see DEVX-102).

## Sources

- [Claude Ship](https://claude.com/resources/articles/introducing-claude-ship)
- [Claude.dev: a practical shipping guide](https://claude.dev/blog/the-work-after-you-open-a-pr/)
