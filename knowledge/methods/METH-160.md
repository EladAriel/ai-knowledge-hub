# METH-160: CapLite: prompt-injection defense without the model writing the policy

## Summary

The policy is derived from the tool schemas, and write actions are locked before the agent reads any tool output. A write is allowed only if every argument that sets the recipient, the amount, or the destination appears explicitly in the user's request. Recommendation: Pilot. Effort: low to medium.

## Details

In CaMeL, Progent and DRIFT the model itself writes the security rules. This paper (arXiv 2611.17115) shows that small models (1.7B to 12B) don't do that reliably, so CapLite takes the model out of that step entirely. Evidence, from the authors, with no public code found: no attack succeeded in 13,935 AgentDojo episodes; under attack, the agent completed tasks at a similar rate to CaMeL (29.0% vs 27.2%), with 18% of the tokens. Effectiveness 4/5, hype 1/5. Fit is high for any agent with tools that write, such as mail, payments or CRM. The review recommends at least adopting the rule that every decisive argument must appear in the user's request. Agent-control has been a recurring topic for several weeks.

## Sources

- [CapLite](https://arxiv.org/abs/2611.17115)
