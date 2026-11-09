# DEVX-003: Haiku 5.5 for subagents and workflows

## Summary

'claude-haiku-5-5' with 1M context at $0.10/$0.50 per Mtok, up to 100K tokens.

## Content

### 3. Haiku 5.5 for subagents and workflows — feasibility for the enterprise: high | Stage: Trial
- **The essence of the change:** `claude-haiku-5-5` with 1M context at $0.10/$0.50 per Mtok, up to 100K tokens.
- **Technical mechanism:** In v2.1.296 `CLAUDE_CODE_WORKFLOW_SUBAGENT_MODEL` was added, and it is also possible to set `model:` in the frontmatter of a subagent.
- **Organizational challenge:** After 100K tokens the price increases 5 times. According to Simon, the new tokenizer counts about 1.25 times tokens. You need to measure before replacing.
- **Practical step (PoC):**
```bash
export CLAUDE_CODE_WORKFLOW_SUBAGENT_MODEL=claude-haiku-5-5
```
- **Success index:** A decrease of 30% or more in the cost of each task (according to `/cost') without a decrease in the pass rate of the tests.
- **Effort:** ~10 minutes
- **Sources:** [v2.1.293](https://github.com/anthropics/claude-code/releases/tag/v2.1.293), [HN (1044 points)](https://news.ycombinator.com/item?id=49996437), [Simon](https://simonwillison.net/2026/Oct/7/claude-haiku-5-5/), [Latent Space](https://www.latent.space/p/ainews-claude-haiku-55-better-than) | Appears in 4 sources Expiration: 2027-01-08

## Sources

- [v2.1.293](https://github.com/anthropics/claude-code/releases/tag/v2.1.293)
- [HN (1044 points)](https://news.ycombinator.com/item?id=49996437)
- [Simon](https://simonwillison.net/2026/Oct/7/claude-haiku-5-5/)
- [Latent Space](https://www.latent.space/p/ainews-claude-haiku-55-better-than)
