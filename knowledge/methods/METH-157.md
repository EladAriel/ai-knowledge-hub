# METH-157: LangChain and Actively AI on "goal engineering": scope agents so humans can easily give feedback

## Summary

Actively moved from one agent per sales account to one agent per job type (a "motion"), such as outbound or early-stage deal progression, so reviewers could batch similar tasks and lessons transferred across accounts. LangChain blog, Nov 14. Effort: medium (a product and UX change).

## Details

Background agents still gather each account's facts. The point is that the most valuable context is unwritten expert judgment, which only arrives as human feedback, so the review UX is the bottleneck. Human-in-the-loop handoff works better when queues are grouped by job type than by entity or customer. Caveat: opinion plus one case study, with no metrics. Rebrand check: "goal engineering" is job-to-be-done scoping plus a human feedback loop plus a shared playbook memory. Adopt for: Architects split fact-gathering context agents (per entity) from acting agents (per job type), with a shared, versioned playbook store per job type; Product design the review queue per job type and measure feedback items per reviewer-hour; Devs tag every trace with a motion / job-type field so feedback and evals can be sliced by it.

## Sources

- [LangChain: goal engineering](https://www.langchain.com/blog/goal-engineering)
