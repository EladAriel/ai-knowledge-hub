# METH-046: Cross-script entity matching fails

## Summary

Same name in a different script breaks LLM identity matching: Qwen2.5-7B 35.1% -> 8.5% (Devanagari/Latin; also Malayalam).

## Details

Agent's reading: Hebrew/English names (Danny Cohen / Danny Cohen) may become two entities (Hebrew not tested). Keep one canonical ID per person/customer from HR/CRM; store transliterated aliases; match on IDs/emails before asking an LLM; add mixed-language name pairs to the golden set.

## Content

**3. [Same Entity, Different Script: cross-script entity matching fails](https://arxiv.org/abs/2610.31407)**
- Writing the same person's name in a different script (Devanagari versus Latin letters) breaks LLM identity matching. Qwen2.5-7B's accuracy at recognizing the same person fell from 35.1% to 8.5%, and the authors saw the same effect with Malayalam.
- For a Hebrew/English org, this suggests "Danny Cohen" and "Danny Cohen" could end up as two separate entities. That's my reading of the pattern, since the paper didn't test Hebrew.
- Adopt for:
  - *Architects:* keep one canonical ID for each person or customer, from your HR system or CRM, and don't let the LLM decide identity on its own.
  - *Product:* add mixed-language name pairs to your golden question set.
  - *Devs:* store transliterated aliases, and match on IDs or emails before asking an LLM.

## Sources

- [Same Entity, Different Script: cross-script entity matching fails](https://arxiv.org/abs/2610.31407)