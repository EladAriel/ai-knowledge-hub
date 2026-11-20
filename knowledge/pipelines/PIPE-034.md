# PIPE-034: Pipeline: end-to-end — gate, then score

## Summary

End-to-end angle (Nov 19): test the whole system the "gate, then score" way. First, hard pass-or-fail checks: no one sees documents they don't have access to; every claim has a source; the system says "I don't know" when the answer isn't there. Only after those pass, score answer quality. Use your real documents, and run each question several times.

## Details

This differs from earlier end-to-end angles (PIPE-007, PIPE-016, PIPE-026), which were about the flow of connectors, routing or a compiled wiki. Today's practice comes from the vendor-demo paper (METH-184): a bank lab's scores were almost the same in every area because scorers were rating how the demo looked, not what the platform could do.

Who owns it: Architects define the pass-or-fail gates (permission leaks, missing citations, failed abstention). Product decides what "quality" means only for platforms that already passed the gates, and requires repeated runs on real documents. Devs run the gates in CI before any quality score is published.

See also EVAL-043 (which stage broke first) and METH-184.

## Sources

- [Vendor demos fool the people scoring them (gate, then score)](https://arxiv.org/abs/2611.24039)
