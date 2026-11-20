# TOOL-049: Repos: deepnote/agent-initiative-benchmark, jordan-gibbs/hyperresearch, zaxiu88888/issue-rag

## Summary

A simulated company for testing when an agent should speak; a deep-research add-on with a citation check before shipping; and RAG over GitHub issues whose key finding is that retrieval raised made-up answers from 1.1% to 20%.

## Details

deepnote/agent-initiative-benchmark, with its company dataset on Hugging Face (deepnote/pagemantle-company-dataset), simulates 11 business tools like Slack, Linear, Notion, HubSpot and Stripe. It also includes an agent harness and two LLM judges. Borrow: a realistic test company for checking when the agent should speak, with no real data needed. Maturity: brand new, with 1 star, created Nov 8, Apache-2.0 for the code, CC BY 4.0 for the 6 GB of data. It comes from a production company. Only 8 of the 50 tasks are public. Best for Devs as a local test bed, and Product for designing scenarios. jordan-gibbs/hyperresearch is a deep-research add-on for Claude Code and Codex, with a 16-step pipeline that ends in a citation check before shipping. Borrow: after the first draft, only targeted edits are allowed, never a full rewrite; copies of the same story count as one source; the citation check is a hard gate before shipping. Maturity: 4.8k stars, MIT, v0.13.2 on Nov 12, installs with `pip install hyperresearch`. Its "#1 on DRACO" claim is self-reported on 10 tasks. On Codex, its tool limits are instructions only, not enforced. Best for Devs and Architects. zaxiu88888/issue-rag is RAG over a project's GitHub issues. It has 95 hand-checked questions and an audit of its LLM judge. Borrow: it reports a range instead of a single score; a confidently wrong answer counts as incorrect, never as partly right. Key finding: adding retrieval raised made-up answers from 1.1% to 20%. Honest "I don't know" answers turned into confident wrong ones. Maturity: 440 stars, MIT, created Nov 1, with one author and no known users yet. Best for Devs as an eval template, and Product for honest metric reporting.

## Sources

- [deepnote/agent-initiative-benchmark](https://github.com/deepnote/agent-initiative-benchmark)
- [PageMantle company dataset](https://huggingface.co/datasets/deepnote/pagemantle-company-dataset)
- [jordan-gibbs/hyperresearch](https://github.com/jordan-gibbs/hyperresearch)
- [zaxiu88888/issue-rag](https://github.com/zaxiu88888/issue-rag)
