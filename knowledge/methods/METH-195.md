# METH-195: Inkling 2 Mini: an agentic coding model that runs locally (Pilot)

## Summary

An open model that is good at agentic coding usually needs a heavy server. Inkling 2 Mini runs the middle layers 3 times for each token (a looped transformer). It has 26.4B parameters, of which 3.4B are active, it runs locally in about 20GB, it supports a context of up to a million tokens, and it works with vLLM from the first day. That means you can run a coding agent or a company agent on your own machines, without sending data out. The maker also measured how the looping affects the model's ability to follow a chain of thought. The DeepSWE score of 48.2% is a vendor claim. The announcement reached 915 points on Hacker News. Recommendation: Pilot. Effort: low. Next step: run it on your own eval against the small model you use today.

## Details

From the Nov 21 methods digest. Source: [Thinking Machines announcement](https://thinkingmachines.ai/news/inkling-2-mini/).

## Sources

- [Inkling 2 Mini](https://thinkingmachines.ai/news/inkling-2-mini/)
