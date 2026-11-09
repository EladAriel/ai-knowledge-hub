# TOOL-010: Repos: kitaru, Laminar, jevals

## Summary

Replay recorded sessions as regression tests; OTel tracing with plain-English 'Signals'; all evals for a trace in one cheap request.

## Details

zenml-io/kitaru (309, Apache-2.0): replays production sessions against your agent answering tool calls from the recording; imports from Langfuse/LangSmith/Braintrust/Phoenix; frozen cohorts, on_miss="fail", CI exit code. lmnr-ai/lmnr (3.4k, Apache-2.0): Signals return JSON per trace from a plain-English behavior; failure clustering, SQL over traces, CI evals; vendor F1 0.835 at ~23x lower cost. openlayer-ai/jevals (105, MIT): one class for offline/monitor/release gate; LangChain test 500/500 agreement, $0.34 vs $28.17 (5 tasks only).

## Content

### [zenml-io/kitaru](https://github.com/zenml-io/kitaru): replay production runs as regression tests
- **What it does:** Records sessions, or imports them  with tool calls answered from the recording.
- **What to borrow:** Immutable "cohort versions," `on_miss="fail"` so replays never call live tools, and a CI command that exits nonzero on failure ([regression-suite guide](https://docs.zenml.io/kitaru/guides/regression-suite)). It has Python and TypeScript SDKs, with adapters for LangGraph, PydanticAI, OpenAI Agents, Claude Agent SDK, Mastra and Vercel AI SDK.
- **Maturity:** 309 stars, 27 forks, Apache-2.0. Last commit on the default `develop` branch was 8 Oct 2026. Self-hosted via Docker or Helm.
- **Best audience:** Devs and Architects (traces stay in your network).

### [lmnr-ai/lmnr](https://github.com/lmnr-ai/lmnr) (Laminar): agent observability with "Signals"
- **What it does:** OpenTelemetry tracing and Signals: behaviors you describe in plain English, returned as JSON in your own schema. It also clusters similar events, offers SQL over traces and evals in CI, and self-hosts with `docker compose up -d`.
- **Evidence:** Laminar's [flow-1 post](https://laminar.sh/blog/flow-1) reports detection F1 of 0.835, versus 0.816 for GPT-6-sol and 0.890 for Claude Opus 5. That is on the vendor's own 523-trace set, at 888 traces per $1 versus 38 for sol. The post also shows a miss. The [Launch HN post](https://news.ycombinator.com/item?id=50154029) describes building eval datasets from failure clusters.
- **Maturity:** 3,417 stars, 250 forks, Apache-2.0. Last commit on `main` was 16 Oct 2026. Not confirmed: whether flow-1 runs self-hosted.
- **Best audience:** Product (failure funnels) and Devs (TypeScript/Python SDKs).

### [openlayer-ai/jevals](https://github.com/openlayer-ai/jevals): evals cheap enough to run on every trace
- **What it does:** Packs all evals for one trace into a single request to a "decision model." It supports local backends (Kev, Laya, Eikos) and falls back to a chat LLM.
- **What to borrow:** An eval is `state()`, `questions()` and `reduce()`. The same class works as an offline metric, a production monitor and an in-loop gate. Re-calibrate when you switch backends.
- **Evidence:** In [LangChain's test](https://www.langchain.com/blog/jev-agent-evals-langsmith), Jev matched human labels on 500 of 500 pass/fail decisions and cost $0.34 total, versus $28.17 for Claude Sonnet 4.6. The test used only 5 weather requests, so treat it as early.
- **Maturity:** 105 stars, 11 forks, MIT. Created 20 Sep 2026; last commit 15 Oct 2026. Python only for now.
- **Best audience:** Devs.

---

## Sources

- [kitaru](https://github.com/zenml-io/kitaru)
- [lmnr](https://github.com/lmnr-ai/lmnr)
- [jevals](https://github.com/openlayer-ai/jevals)
- [regression-suite guide](https://docs.zenml.io/kitaru/guides/regression-suite)
- [flow-1 post](https://laminar.sh/blog/flow-1)
- [Launch HN post](https://news.ycombinator.com/item?id=50154029)
- [LangChain's test](https://www.langchain.com/blog/jev-agent-evals-langsmith)