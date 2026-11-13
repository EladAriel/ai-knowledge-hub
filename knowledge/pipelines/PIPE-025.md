# PIPE-025: Pipeline: feedback and monitoring (trace → score → route fix → versioned write)

## Summary

trace each request -> score a sample with automatic checks -> find which stage failed -> send the fix to the right place (KB, memory, prompt, index) -> write only when confident, with version history -> alert when quality drifts.

## Details

Trace more than latency (chunk IDs + scores); alert separately on retrieval/generation/system errors; change memory/KB from feedback only when confident and give rarely used items a chance (MEMOIR); screen injection/spam with a cheap gate on the full candidate pool; give every stored rule a scope (Memory Trap); version embedding model, index, prompts and memory. Owners: Architects (trace format, gate placement, versioning); Product (route thumbs-downs, fix latency targets); Devs (OTel traces, cheap decision models, CI on past failures, A/B feedback on/off).

## Sources

- No external source link (in-house technique note).
