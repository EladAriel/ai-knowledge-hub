# METH-008: An Empirical Study of Harness Design for Coding Agents

## Summary

What it is: A controlled study. The execution loop of the code agent remains constant, and only three components are changed: planning, scope of operations and context management. 176 definitions were tested on four models, in SWE-Bench Verified and Terminal-Bench 2.1. - Why new: This is the first time that harness components are measured individually.

## Content

**1. [An Empirical Study of Harness Design for Coding Agents](https://arxiv.org/abs/2609.20804)**
- **What it is:** A controlled study. The execution loop of the code agent remains constant, and only three components are changed: planning, scope of operations and context management. 176 definitions were tested on four models, in SWE-Bench Verified and Terminal-Bench 2.1.
- **Why new:** This is the first time that harness components are measured individually. The article was published on 17.9 and gained momentum in X on 11.10 ([the post](https://x.com/vinhnx/status/2109084805753410029) gained about 3.8K likes).
- **Evidence:**
  - Context management pays off mainly when the window is crowded, and even then most of the benefit is preventing browsing.
  - The most effective was to trim according to rules before concluding with an LLM.
  - The option to restore content that was cut was almost never used.
  - Planning helps weak models, and in strong models it mainly saves cost.
  - A model that is good in bash gets along with the bash interface only, and at a lower cost.
  - I couldn't find a link to the code.
- **Scores:** Effectiveness 4/5, Hype 3/5.
- **Compatibility:** Suitable for any agent product. **low** effort.
- **Recommendation: Adopt**

## Sources

- [An Empirical Study of Harness Design for Coding Agents](https://arxiv.org/abs/2609.20804)
- [the post](https://x.com/vinhnx/status/2109084805753410029)
