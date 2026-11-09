# METH-093: Signed but Steerable: signed knowledge-pack vectors can still lie

## Summary

Some knowledge packs ship text plus ready-made vectors; a signature proves who published the pack, not that the vectors match the text, so tampered vectors can hijack retrieval. In a FAISS index with compressed vectors, tampered vectors passed the audit and put the attacker's doc first for 25% of targets; answer accuracy on a device fell from 0.75 to 0.39.

## Details

Their fix: check the stored compressed vectors themselves. Effort: medium. Adopt for: Architects never index embeddings a vendor supplies — re-embed the text yourself; Product lists which sources arrive with ready-made vectors; Devs add a CI check that re-embeds a sample and flags any mismatch. Same finding as the Margin law term in the Nov 5 AI methods digest.

## Sources

- [Signed but Steerable / Margin law (arXiv)](https://arxiv.org/abs/2611.06498)
- [code](https://github.com/securagenai/signed-but-steerable)
