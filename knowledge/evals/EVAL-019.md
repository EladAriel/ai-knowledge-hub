# EVAL-019: SWE-Shift: Agents when the world shifts mid-mission

## Summary

A benchmark where the code, dependencies, or requirements change while the agent is running.

## Content

**2. [SWE-Shift: Agents when the world shifts mid-mission](https://arxiv.org/abs/2610.32196)**
- **What it is:** A benchmark where the code, dependencies or requirements change while the agent is running. It has 120 scenarios in 12 families of changes.
- **Why new:** Most benchmarks assume that the environment is frozen. Here it is explicitly measured if the agent maintains the work that is still valid, and if he refreshes evidence that has become obsolete.
- **Evidence:**
  - All 17 tested systems fail. GPT-6 Astra drops from 67% to 25%.
  - In changes to the tool or the session, and in tasks with outdated evidence, no system was successful.
  - No external recovery yet.
- **Scores:** Effectiveness 4/5, hype 1/5.
- **Fit:** High for any product that works with live data. **medium** effort.
- *... for the full report. This continues HDA from 19.10.

## Sources

- [SWE-Shift: Agents when the world shifts mid-mission](https://arxiv.org/abs/2610.32196)
