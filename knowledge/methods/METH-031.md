# METH-031: SAFE-Mem: memory with kind/authority/scope labels

## Summary

Each stored claim labeled with kind (fact/preference/policy), authority and scope; it only influences answers when labels fit.

## Content

**3. [SAFE-Mem: memory with authority and scope labels](https://arxiv.org/abs/2610.22959)** (arXiv, Oct 16)
- **How it works:** each stored claim gets three labels. Kind says whether it's a fact, preference, or policy. Authority says who said it, and scope says where it may be used. A claim only influences an answer if its labels fit the question.
- **Why it matters:** this blocks an attack where text from an email or webpage gets saved and later acts like a user preference or a permission. They report at least 77% lower attack success than the strongest defense that still keeps legitimate memory, and up to 15 points better accuracy.
- The code is public, but the repo has 1 star, so treat it as a reference only.
- This is the third time "check permissions outside the model" has come up, now for memory.
- Adopt for:
  - *Architects:* add authority and scope fields to the memory data contract.
  - *Product:* decide which sources are allowed to create "policy" memories.
  - *Devs:* write a test where an injected doc tries to become a user preference.

## Sources

- [SAFE-Mem](https://arxiv.org/abs/2610.22959)
