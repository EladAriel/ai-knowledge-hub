# PIPE-014: Pipeline: gated agent/answer layer with code checks

## Summary

question -> gate (answer/clarify/decline) -> template or retrieval -> pack evidence -> grounded generation with citations -> code checks -> confirm before writes -> response + trace.

## Details

Gate first; serve common questions s more confident than sources); keep disagreements visible.

## Content

## Pipeline pattern of the day: agent/answer layer

question -> gate decides answer, clarify or decline -> template answer, or retrieval -> pack the evidence -> grounded generation with citations -> code checks -> confirm before any write -> response plus trace

- **Gate first.** Decide whether to answer, ask a clarifying question or decline before generating anything, and serve common questions from fixed templates ([Governed Sovereign RAG](https://arxiv.org/abs/2610.36561)).
- **Pack evidence with its structure.** [Tessera](https://arxiv.org/abs/2610.37080) rebuilds retrieved pages into small units that keep their title, section path and table headers. That added 5–6 points of accuracy at the same token budget, without changing the index or the retriever.
- **Check the evidence is enough.** List the facts the question needs, and answer only when every one is covered. [Certify](https://arxiv.org/abs/2610.34684) got 80% right using its smallest sufficient set of passages, versus 57% using all retrieved passages.
- **Check facts in code.** Numbers, codes and IDs in the answer must appear in the sources, and the runtime enforces the confirmation steps for writes, as in Concordat.
- **Watch for "claim smoothing."** [Durrett's group](https://arxiv.org/abs/2610.35793) found research agents write conclusions more confident than their sources. Keep disagreements between sources visible in the answer.
- **Who owns it:**
  - *Architects* own the gate rules, the list of code checks and the write-action protocols, as versioned config.
  - *Product* owns the list of question types, which ones get templates, and the experience of clarifying or declining. Its metrics are drop-off and resolution rate.
  - *Devs* own the evidence packing, the code checks and the tool filtering, each with unit tests.

## Sources

- [Tessera](https://arxiv.org/abs/2610.37080)
- [Certify](https://arxiv.org/abs/2610.34684)
- [claim smoothing](https://arxiv.org/abs/2610.35793)
- [Governed Sovereign RAG](https://arxiv.org/abs/2610.36561)