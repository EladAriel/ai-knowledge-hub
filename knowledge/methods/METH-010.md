# METH-010: Lost in Implicit Routing: collapse in routing skills

## Summary

As there are more irrelevant skills, the agent stops loading the relevant skills as well, even though they are installed.

## Content

### 1. [Lost in Implicit Routing: collapse in routing skills](https://arxiv.org/abs/2610.18522)
[code](https://github.com/jinlinll/lost-in-implicit-routing)

- **What is it:** The more irrelevant skills there are, the agent stops loading the relevant skills as well, even though they are installed.
- **The data:** With 1,000 distracting skills, the recall drops  does not claim any skill. When you explicitly choose skills in advance, the recall remains at about 73.9%.
- **Why new:** This is a new measurable finding, which complements One Skill Too Many  claims less than necessary.
- **Evidence:** Over 15K routes on 3 open models, with partial validation on Claude, Gemini and GPT.
- **Scores:** Effectiveness 5/5, hype 2/5.
- **Compatibility and effort:** High for any product with a skills library. **low to moderate** effort.
- **Recommendation: Adopt.** You should measure how many of the relevant skills were really loaded, and not just if the task was passed. When there are about 100 skills or more, you should add an early selection stage.

## Sources

- [Lost in Implicit Routing: collapse in routing skills](https://arxiv.org/abs/2610.18522)
- [code](https://github.com/jinlinll/lost-in-implicit-routing)
