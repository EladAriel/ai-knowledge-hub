# PIPE-023: Pipeline: event-driven ingestion with page hashes, resume and a completion marker

## Summary

Third pass on ingestion and connectors: change event -> priority queue -> did the document change? -> which pages/chunks changed? -> embed only those -> save -> mark the document complete -> searchable. Events not polling, idempotent syncs, completion marker, freshness measured per source.

## Details

Stages: change event from the source -> priority queue -> did the document change? -> which pages or chunks changed? -> embed only those -> save -> mark the document complete -> it becomes searchable.
- Use events, not polling, with separate queues for live uploads and bulk syncs so a big backfill can't stall urgent work (PULSAR).
- Make syncs safe to repeat: document- and chunk-level hashes, delete leftover chunks when a document gets shorter, resume from the last saved part after a crash.
- Completion marker: hide a document from search until every part is indexed.
- Measure freshness: time from change to searchable per source; alert on the worst hour, not the average.
- Question whether you need to parse at all: for visual documents, indexing page images can beat OCR on cost and accuracy; test on your own documents first.
Who owns it: Architects own the ingestion contract (event format, hash keys, completion marker, freshness targets, indexed vs fetched-live sources); Product sets freshness targets per use case (seconds for live deals, hourly for policies) and picks the first 1-2 sources; Devs build the worker with hashing, resume and cleanup plus a test that runs each sync twice.
New terms: page-hash resume, completion marker, idempotent sync. Related: PIPE-008 (Oct 22) and PIPE-017 (Oct 31) ingestion pipelines.

## Content

## Pipeline pattern of the day: ingestion and connectors

change event from the source -> priority queue -> did the document change? -> which pages or chunks changed? -> embed only those -> save -> mark the document complete -> it becomes searchable

- **Use events, not polling,** with separate queues for live uploads and bulk syncs. That way one big backfill can't stall urgent work (PULSAR).
- **Make syncs safe to repeat.** Use hashes at document and chunk level, delete leftover chunks when a document gets shorter, and resume from the last saved part after a crash.
- **Use a completion marker.** Hide a document from search until every part of it is indexed.
- **Measure freshness.** Track how long a change takes to become searchable for each source, and alert on the worst hour, not the average.
- **Question whether you need to parse at all.** For visual documents, indexing page images can beat OCR on both cost and accuracy. Test it on your own documents first.
- **Who owns it:**
  - *Architects* own the ingestion contract: the event format, hash keys, the completion marker and the freshness targets. They also decide which sources get indexed and which get fetched live.
  - *Product* sets freshness targets per use case, like seconds for live deals and hourly for policies, and picks the first 1–2 sources.
  - *Devs* build the worker with hashing, resume and cleanup, plus a test that runs each sync twice.

## New terms
- **Late interaction:** each document keeps many vectors, and each word of the query is matched to its best one.
- **Vision-first RAG:** indexing pictures of pages instead of text pulled out with OCR.
- **Page-hash resume:** re-embedding only pages whose content changed, and continuing from the last saved page after a crash.
- **Completion marker:** a document becomes searchable only once every part of it is saved.
- **Verified memory release:** removing a memory from search only after a test shows it's no longer needed.
- **Near-duplicate crowding:** copies of the same content filling your top results.
- **Idempotent sync:** running a sync twice gives you the same index.

**Recurring themes:**
- Prove nothing is lost before you compress or forget, now three days in a row.
- Every bug becomes a test.
- Ranking with no LLM involved, with only a small model as a filter.

## Sources

- [PULSAR (arXiv 2608.28572)](https://arxiv.org/abs/2608.28572)
