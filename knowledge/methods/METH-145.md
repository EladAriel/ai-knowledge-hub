# METH-145: DISCERN: keep everything when saving, decide when reading

## Summary

On a synthetic sales-agent memory benchmark (310 questions), plain RAG already scores about 0.93–0.98 at keeping facts current, so recall is basically solved. What breaks is resolution: which "Acme" the user means, which value is current, and when to decline. Effort: medium. Also rated Pilot in a Nov 14 methods review.

## Details

The fix (arXiv 2611.15729): never merge look-alike entities or delete old values when saving. Keep each fact's dates and source (a bi-temporal provenance graph), and decide when answering with a tool loop that makes no LLM calls. Results: deciding when to decline scored 0.924 F1, versus at most 0.802 for 8 other approaches; telling look-alike entities apart scored 0.800, where no other approach beat 0.40. Limits: the main benchmark is synthetic, and there's no code yet. Adopt for: Architects make the memory store append-only with valid-from/valid-to fields, and resolve at query time; Product count a correct "I don't know" as a success; Devs add look-alike pairs, like two Acmes or two Johns, to your golden questions. A Nov 14 methods review covers the same paper as a Pilot, as part of a recurring memory-with-source-tracking theme (Anthropic Nov 8, WikiTrace and FGSE Nov 11, MAPE Nov 13).

## Sources

- [DISCERN](https://arxiv.org/abs/2611.15729)
