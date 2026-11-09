# EVAL-002: RBC: Randomized Block Curation

## Summary

A method to check which parts of the playbook the agent wrote for himself (like ACE or Dynamic Cheatsheet) really help.

## Content

### 1. [RBC: Randomized Block Curation](https://arxiv.org/abs/2610.18427)
- **What it is:** A method to check which parts of the playbook the agent wrote for himself (like ACE or Dynamic Cheatsheet) really help. Blocks are randomly added and omitted on practice tasks, and success in the task is measured. Do not trust the self-judgment of the model.
- **Why new:** This is a random experiment on memory that the agent wrote himself. It is neither RAG nor Reflexion.
- **Evidence:** Tested in 19 settings, on 3 models and 3 benchmarks. The average score with the method is 66.9. With the full playbook the score is 55.5, without a playbook at all 54.1, and with self-judgment 53.8. The code is posted anonymously.
- **Scores:** Effectiveness 5/5, hype 2/5.
- **Compatibility:** Very high. **medium** effort.
- **Recommendation: Adopt**

## Sources

- [RBC: Randomized Block Curation](https://arxiv.org/abs/2610.18427)
