# TOOL-002: Microsoft Execution Containers (MXC)

## Summary

What it is: An isolation layer for Windows agents. A policy determines which files and network destinations the agent can access, and MXC enforces it at runtime. The version reached 1.0 GA. - Why new: sandboxing is not a new idea. The innovation is an OS-level policy built specifically for local agents, and whose identity will be connected to Entra and Agent 365.

## Content

**1. Microsoft Execution Containers (MXC)** (https://blogs.windows.com/windowsdeveloper/2026/10/07/microsoft-execution-containers-policy-driven-containment-for-ai-agents/)
- **What it is:** An isolation layer for agents in Windows. A policy determines which files and network destinations the agent can access, and MXC enforces it at runtime. The version reached 1.0 GA.
- **Why new:** sandboxing is not a new idea. The innovation is an OS-level policy built specifically for on-premises agents, whose identity will be connected to Entra and Agent 365.
- **Evidence:** Open source (about 2.6K stars) and official GA. There are no independent security measures, and the connection to Entra is still only announced.
- **Scores:** Effectiveness 4/5, Hype 2/5.
- **Compatibility and effort:** Suitable for any product that runs an agent on the customer's computer. **medium** effort.
- **Recommendation: Pilot**

## Sources

- [Microsoft Execution Containers (MXC)](https://blogs.windows.com/windowsdeveloper/2026/10/07/microsoft-execution-containers-policy-driven-containment-for-ai-agents/)
- [repo](https://github.com/microsoft/mxc)
