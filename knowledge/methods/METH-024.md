# METH-024: EGCForest: multi-view memory for enterprise group chats

## Summary

Append-only chat log with derived views by channel, speaker and artifact; up to +20.85 accuracy points over MemOS.

## Details

Links connect the views. No code found. Model chat as an append-only log plus derived views, never overwrite with summaries; cheap first step: add speaker and artifact metadata at ingestion. Fits 'who owns X now?' / 'what was decided?'.

## Content

**3. [EGCForest: structured memory for enterprise group chats](https://arxiv.org/abs/2610.19836)**
- **What:** it organizes Slack-style chat into three views over one log that never changes. The views are by channel (how work moves over time), by speaker (who said it and with what authority), and by artifact (how a deliverable evolves). Links connect the views.
- **Results:** on three enterprise-chat benchmarks it beat RAG and memory baselines, by up to 20.85 accuracy points over MemOS, another memory system. I found no code.
- Adopt for:
  - *Architects:* model chat as an append-only log plus derived views, and never overwrite it with summaries.
  - *Product:* questions like "who owns X now?" and "what was decided?" are where this fits.
  - *Devs:* even without the paper's code, adding speaker and artifact metadata at ingestion is cheap.

## Sources

- [EGCForest](https://arxiv.org/abs/2610.19836)