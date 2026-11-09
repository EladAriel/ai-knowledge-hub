# METH-046: Cross-script entity matching fails

## Summary

Same name in a different script breaks LLM identity matching: Qwen2.5-7B 35.1% -> 8.5% (Devanagari/Latin; ….

## Details

Note: Hebrew/English names ( / Danny Cohen) may become two entities (Hebrew not tested). Keep one canonical ID per person/customer from HR/CRM; store transliterated aliases; ….

## Sources

- [Same Entity, Different …](https://arxiv.org/abs/2610.31407)
