# TOOL-050: Repos: ratel-ai/ratel, OCNAI/kebivo, thenexuslab/stalebench-release

## Summary

A self-hosted console for what your agent is getting wrong; an inbox for questions your AI couldn't answer; and the frozen evaluator behind StaleBench, including a freshness metric for memory.

## Details

ratel-ai/ratel ingests OTLP traces plus the agent's catalog of tools and skills. From that traffic it derives agent-health signals, self-corrections, topics, intent clusters / an intent graph ("what people ask for") and match quality. It runs as one app plus Postgres, and works without a model key (model-based readings are then skipped). Borrow: intent clustering over real traffic as the input to gap mining, and the "no outbound model call by default" setup. Maturity: 566 stars, 33 forks, TypeScript and Rust. MIT per the GitHub API; the README badge says Apache-2.0 & MIT. Last commit 2026-11-18 02:11 (Asia/Jerusalem). Quick start: `docker compose up -d --build --wait`, then localhost:3000. 26 open issues. Best for Devs (self-hosted trace analytics) and Product (what users ask for).

OCNAI/kebivo: your RAG or chat app reports each unanswered question over REST or MCP. Kebivo groups the repeats with a count and routes them to content owners via Slack, email or webhook. One container, self-hosted. Borrow: the report → dedupe into groups → route to owner contract. This is today's eval (EVAL-042) in product form. Maturity: early and tiny — 1 star, 0 forks, v0.3.0, Apache-2.0. Last commit 2026-11-12 02:26 (Asia/Jerusalem), pushed Nov 17. Has CI, migrations, e2e compose files, and a docker-run quick start. Borrow the design; don't depend on it yet. Best for Product and Architects.

thenexuslab/stalebench-release has the data, frozen evaluator, harness and result records behind StaleBench (METH-175), including adapters and results for Mem0, Graphiti and LangMem. Borrow: the contamination@5 metric and the current@1 / stale@1 split as a freshness monitor for any memory or knowledge-graph store. Maturity: 0 stars (new), Apache-2.0, created Nov 15, last commit 2026-11-15 04:52 Asia/Jerusalem ("1.2.2: sync with camera-ready"). Zenodo archive. Paper accepted to Findings of EACL 2027. Best for Devs and Architects choosing a memory layer.

## Sources

- [ratel-ai/ratel](https://github.com/ratel-ai/ratel)
- [OCNAI/kebivo](https://github.com/OCNAI/kebivo)
- [thenexuslab/stalebench-release](https://github.com/thenexuslab/stalebench-release)
