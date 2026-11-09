# METH-099: New terms (Nov 5): Coca-Cola latent tool tokens, Germline MCP, HarnessFlow, EvoGuard, Turn-level Best-of-N, BudgetMix RL, Compression weakens refusal

## Summary

One-line mentions from the Nov 5 AI methods digest (no full evaluations).

## Details

Coca-Cola (arXiv 2611.06500, code THU-Agent/Coca-cola): compress tool output to latent tokens instead of text; claimed 70%–89% token savings. Germline execution (2611.06585): every MCP tool call runs in a clean process copy with no data, so a signed-but-malicious tool cannot leak — continues yesterday's supply-chain wave. HarnessFlow (2611.06254): MCTS search over whole harnesses; claimed +3.95 points over Meta-Harness. EvoGuard (2611.06444): pairwise classifier that decides whether to adopt a new skill version during online evolution. Turn-level Best-of-N (2611.06868): one model proposes N actions per step, another picks; +5%–10% on terminal tasks. BudgetMix RL (2611.06483): vary step budget during RL training because RL gains vanish when the budget shrinks. Compression weakens refusal (2611.06380): context compression weakens refusal behavior even when reconstruction is faithful. Also noted: Kimi K3.1 Pro open weights (2.8T MoE); NVIDIA Auto Ontology still Watch; vercel-labs/agent-desktop still trending.

## Content

**New names and terms**
- [Coca-Cola](https://arxiv.org/abs/2611.06500): Compress tools output to latent tokens instead of text. According to the article saves 70% to 89% of tokens ([code](https://github.com/THU-Agent/Coca-cola)).
- [Germline execution](https://arxiv.org/abs/2611.06585): Every call to the MCP tool ran in a clean copy of a process with no data, so a signed but malicious tool cannot leak. Continuing the supply chain wave from yesterday.
- [HarnessFlow](https://arxiv.org/abs/2611.06254): MCTS search on complete harnesses. According to the article beats Meta-Harness by 3.95 points.
- [EvoGuard](https://arxiv.org/abs/2611.06444): A pairwise classifier that decides whether to adopt a new version of a skill, to prevent degradation during online evolution.
- [Turn-level Best-of-N](https://arxiv.org/abs/2611.06868): One model generates N actions at each turn and another model chooses between them. 5% to 10% improvement in terminal tasks.
- [BudgetMix RL](https://arxiv.org/abs/2611.06483): Changing the budget of steps during RL training for agents, because according to the article the profit from RL disappears when the budget is small.
- [Margin law](https://arxiv.org/abs/2611.06498): Signing a RAG knowledge pack does not prove that the vectors match the text.
- [Compression weakens refusal](https://arxiv.org/abs/2611.06380): Context compression weakens the refusal behavior, even when the reconstruction is faithful.
- [Kimi K3.1 Pro](https://huggingface.co/moonshotai/Kimi-K3.1-Pro): open weights, 2.8T parameters, MoE.
- **From yesterday / from 3.11:** [NVIDIA Auto Ontology](https://github.com/NVIDIA/auto-ontology) received 2,050 stars per day. Still no numbers in the README, and Watch remains. [vercel-labs/agent-desktop](https://github.com/vercel-labs/agent-desktop) also continues the trend: computer use through the accessibility tree instead of screenshots.

## Sources

- [Coca-Cola](https://arxiv.org/abs/2611.06500)
- [code](https://github.com/THU-Agent/Coca-cola)
- [Germline execution](https://arxiv.org/abs/2611.06585)
- [HarnessFlow](https://arxiv.org/abs/2611.06254)
- [EvoGuard](https://arxiv.org/abs/2611.06444)
- [Turn-level Best-of-N](https://arxiv.org/abs/2611.06868)
- [BudgetMix RL](https://arxiv.org/abs/2611.06483)
- [Margin law](https://arxiv.org/abs/2611.06498)
- [Compression weakens refusal](https://arxiv.org/abs/2611.06380)
- [Kimi K3.1 Pro](https://huggingface.co/moonshotai/Kimi-K3.1-Pro)
- [NVIDIA Auto Ontology](https://github.com/NVIDIA/auto-ontology)
- [vercel-labs/agent-desktop](https://github.com/vercel-labs/agent-desktop)