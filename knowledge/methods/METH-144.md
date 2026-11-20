# METH-144: Isolation Is Not Confidentiality: embedding-transform access control is not secrecy

## Summary

Some vector databases enforce access by transforming embeddings per policy, so a user only matches vectors from their own group. Isolation holds, but it isn't the same as keeping data secret. Effort: low (a design decision, not a build).

## Details

The authors tested the public versions (arXiv 2611.14061). A curious user can recover the original embeddings from a few hundred pairs, can forge queries for other policies (costly but possible), and the geometry itself shows which policy a document belongs to. Tricks with embeddings don't replace a real permission check, and stored vectors should be treated as sensitive data. Adopt for: Architects list four separate requirements in the threat model — users are kept apart, data stays secret, queries can't be forged, and nobody can tell which group a document belongs to; Product should not promise customers their data is "encrypted in the index" when it's only kept apart; Devs keep the permission check in code, not in the embeddings.

## Sources

- [Isolation Is Not Confidentiality](https://arxiv.org/abs/2611.14061)
