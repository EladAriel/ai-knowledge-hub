# METH-093: Signed but Steerable: signed knowledge-pack vectors can still lie

## Summary

Some knowledge packs ship text plus ready-made vectors; a signature proves who published the pack, not that the vectors match the text, so tampered vectors can hijack retrieval. In a FAISS index with compressed vectors, tampered vectors passed the audit and put the attacker's doc first for 25% of targets; answer accuracy on a device fell from 0.75 to 0.39.

## Content

**4. [Signed but Steerable: signed vectors can still lie](https://arxiv.org/abs/2611.06498)** ([code](https://github.com/securagenai/signed-but-steerable))
- **The problem:** some knowledge packs ship text plus ready-made vectors. A signature on the pack proves who published it, not that the vectors match the text, so tampered vectors can hijack retrieval.
- **Results:** in a FAISS index with compressed vectors, tampered vectors passed the audit and still put the attacker's doc first for 25% of targets. Answer accuracy on a device fell from 0.75 to 0.39.
- **Their fix:** check the stored compressed vectors themselves.
- Adopt for:
  - *Architects:* never index embeddings a vendor supplies. Re-embed the text yourself.
  - *Product:* list which sources arrive with ready-made vectors.
  - *Devs:* add a CI check that re-embeds a sample and flags any mismatch.

**New names and terms**
- [Margin law](https://arxiv.org/abs/2611.06498): Signing a RAG knowledge pack does not prove that the vectors match the text.

## Sources

- [Signed but Steerable / Margin law (arXiv)](https://arxiv.org/abs/2611.06498)
- [code](https://github.com/securagenai/signed-but-steerable)
