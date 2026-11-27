# METH-206: Permission-aware RAG, with a demo you can run

## Summary

Teams tell the model "don't share confidential docs" in the prompt. In this demo, rewording the question gets around that rule, while the same rule blocks a normal question a user is allowed to ask. The fix is that code decides access before the model sees anything. Each chunk carries the document's access list, and a chunk with no list is hidden from everyone. The server looks up the user's groups, and the filter runs inside the search. The cache is keyed by permission set, and a persona-by-document test matrix runs in CI. Why it matters: it gives you a clear threat model and test layout. It compares 3 pipelines (a prompt rule, a filter after the top results, and a filter inside the search) on 17 fake docs. The default model is scripted, so this shows the design, not real model numbers. The repo is MIT-licensed and brand new, with no stars yet. Next step: copy its persona-matrix test style into your own CI. For: architects and devs.

## Details

Reported Nov 24. Complements today's permissions practice in PIPE-039 and the leak test in EVAL-047.

## Sources

- [Permission-aware RAG (Witty Programming)](https://wittyprogramming.dev/articles/permission-aware-rag/)
- [kzagoris/permission-aware-rag](https://github.com/kzagoris/permission-aware-rag)
