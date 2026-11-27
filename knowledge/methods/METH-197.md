# METH-197: Canary tokens in the inference chain (Adopt)

## Summary

Prompts travel through routers and resellers. Every stop along the way sees the whole prompt, and a zero-data-retention (ZDR) promise is mostly a promise. For 5 months, about 2 million prompts were sent with unique secrets (links and fake AWS keys), and the researchers checked where those secrets showed up later. They found 3 providers that had been breached, resellers that had stored prompts, and requests to US providers that reached organizations in China. OpenRouter removed 3 providers and took 125 endpoints off the ZDR list. Together, Novita and Phala published notices. An enterprise product that goes through an aggregator cannot assume ZDR actually holds. The method is simple to copy, and these are documented findings, not marketing. Recommendation: Adopt. Lock a list of approved providers, and add canary tokens to ongoing tests. Effort: low to medium.

## Details

From the Nov 22 methods digest. Sources: [Dragos](https://dragos.com/blog/ai-supply-chain-security-canary-tokens) · [OpenRouter](https://openrouter.ai/blog/announcements/data-processing-incidents-on-inference-providers/).

Practical note: if you add OpenRouter (or any router) to your stack, give the router a list of approved providers.

Terms from the same digest: prompt canary tokens are a unique secret inside a prompt that shows whether it leaked further down the chain; OpenRouter now returns an endpoint to ZDR only after verification (ZDR eligibility).

## Sources

- [Dragos: canary tokens in the AI supply chain](https://dragos.com/blog/ai-supply-chain-security-canary-tokens)
- [OpenRouter: data-processing incidents](https://openrouter.ai/blog/announcements/data-processing-incidents-on-inference-providers/)
