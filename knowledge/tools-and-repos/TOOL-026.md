# TOOL-026: Repos: Langfuse, Opik, Phoenix

## Summary

Tracing + evals platforms: live-trace judge rules, online evaluation rules, vendor-neutral OpenInference tracing.

## Details

langfuse/langfuse (~36.7k, MIT except ee/, now ClickHouse): judge rules on live traces, bad traces -> datasets for regression. comet-ml/opik (~23k, Apache-2.0 incl. backend): online evaluation rules sampling production traffic; self-host ./opik.sh. Arize-ai/phoenix (~12k, Elastic License 2.0): OTel/OpenInference tracing, no vendor lock-in.

## Content

**[langfuse/langfuse](https://github.com/langfuse/langfuse)** handles tracing, prompt management, datasets and LLM-as-judge evals.
- What to borrow: judge rules that score live traces, plus turning bad traces into datasets for regression runs.
- Maturity: high. About 36.7k stars, and v4.71.0 shipped Oct 27. It's MIT except the `ee/` folders, and the copyright now belongs to ClickHouse, Inc.
- Best for: Devs and Product.

**[comet-ml/opik](https://github.com/comet-ml/opik)** covers tracing, experiments, evaluation rules on live traffic, and guardrails.
- What to borrow: its [online evaluation rules](https://www.comet.com/docs/opik/production/online-evaluation/rules/), which sample and score production traffic.
- Maturity: high. About 23k stars, release 2.2.131 shipped Oct 28, and it's Apache-2.0 including the backend. Self-host with `./opik.sh` (Docker) or `pip install opik`.
- Best for: Architects who need a self-hosted option with a fully permissive license.

**[Arize-ai/phoenix](https://github.com/Arize-ai/phoenix)** does tracing and evals on OpenTelemetry and OpenInference, its open standard for LLM traces.
- What to borrow: tracing that doesn't lock you into one vendor, so you can switch backends later.
- Maturity: high. About 12k stars, evals v3.9.5 released Oct 28. Run it with `pip install arize-phoenix` and then `phoenix serve`.
- License: Elastic License 2.0, so check it before offering Phoenix as a hosted service.
- Best for: Devs.

## Sources

- [langfuse](https://github.com/langfuse/langfuse)
- [opik](https://github.com/comet-ml/opik)
- [phoenix](https://github.com/Arize-ai/phoenix)
- [online evaluation rules](https://www.comet.com/docs/opik/production/online-evaluation/rules/)