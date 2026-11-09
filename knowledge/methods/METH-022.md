# METH-022: Environment-Agnostic Coding Agents: The Role of Scaffolding

## Summary

A small change in the prompt, 'stop and report when unsure', improves scores on the ARC-AGI-3 and the AGI Maze without a scaffold that is adapted to the environment.

## Content

### 5. [Environment-Agnostic Coding Agents: The Role of Scaffolding](https://arxiv.org/abs/2610.22289)
[EnvTraverse](https://github.com/astroseger/envtraverse)
- **What it is:** A small change in the prompt, "Stop and report when you are not sure", improves scores in ARC-AGI-3 and AGI Maze without a scaffold that is adapted to the environment. There still remains a gap against an agent built specifically for ARC.
- **Why new:** The finding is that the agent has information and tools but doesn't use them, and a small prompt change works in several different environments.
- **Evidence:**
  - Tested on GPT-5.5 and GPT-5.6-sol.
  - The cost of tokens increases along with the improvement.
  - It is not clear if the improvement comes from a better use of information or simply unnecessary inference.
- **Scores:** Effectiveness 3/5, Hype 2/5.
- **Suitability:** Medium to high for code agents. **low** effort.
- **Recommendation: Pilot**

## Sources

- [Environment-Agnostic Coding Agents: The Role of Scaffolding](https://arxiv.org/abs/2610.22289)
- [EnvTraverse](https://github.com/astroseger/envtraverse)
