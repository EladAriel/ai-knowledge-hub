# METH-136: Dependable long-horizon LLM agents: where errors enter, and don't invent a final answer

## Summary

The authors read 95 failed multi-agent runs from start to finish. Errors usually start early (a median of 18% of the way into a run). In 37 of 88 runs the error came before the step human reviewers had labeled as the cause. In 72% of failed runs, evidence against the error was already in the run's history; in 88% of those, no agent used it. In 45% of Who&When failures, the provider's content filter crashed the run and the surrounding code printed a 'final answer' no agent had written.

## Details

They share their method and scripts. Effort: low, since it's a way of reviewing failures. Adopt for: Architects—fix the task's requirements at the start, and add a separate checker that compares what the agent believes against the real systems; Product—when prioritizing fixes, sort failures by where the error started, not only by what the user saw; Devs—when a provider returns an error, fail loudly, and never let the code fill in a made-up final answer. In an agent harness, this means recording the outcome as a failure with a reason such as provider_error, never a fallback final answer. arXiv 2611.13254.

## Sources

- [Dependable long-horizon agents (arXiv)](https://arxiv.org/abs/2611.13254)
