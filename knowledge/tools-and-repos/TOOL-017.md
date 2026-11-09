# TOOL-017: Repos: LangExtract, cognee, Splink

## Summary

Source-grounded LLM extraction; ontology-checked memory/KG layer; probabilistic record linkage.

## Details

google/langextract (~39k, Apache-2.0): every value tied to exact char position; HTML review page; drop values with char_interval=None. topoteretes/cognee (~32.7k, Apache-2.0): checks entities against your ontology, annotate vs strict modes, can run without an LLM. moj-analytical-services/splink (~2.5k, MIT): blocking rules and match weights on DuckDB/Spark/Postgres; most 'LLM entity resolution' is classic record linkage, start here.

## Content

**[google/langextract](https://github.com/google/langextract)** does LLM extraction where every value is tied to its exact character position in the source. It also produces an HTML page for reviewing the results.
- What to borrow: its rule that a value with no source location (`char_interval = None`) can be dropped.
- Maturity: about 39k stars, Apache-2.0, release v1.7.1 on Oct 8, with a `pip install` quickstart.
- Best for: Devs, and Product, since the HTML review page works well for domain experts.

**[topoteretes/cognee](https://github.com/topoteretes/cognee)** is an open-source memory and knowledge-graph layer that checks extracted entities against your ontology. Its "annotate" mode keeps entities that don't fit the ontology and flags them, and its "strict" mode drops them.
- What to borrow: the two modes, plus the option to run it without an LLM for a quick local trial.
- Maturity: about 32.7k stars, Apache-2.0, pushed Oct 23 (v1.6.6rc1), with a `uv`/`pip` quickstart. The SDK includes Google Drive and Gmail connectors.
- Best for: Architects designing the ontology, and Devs.

**[moj-analytical-services/splink](https://github.com/moj-analytical-services/splink)** is fast probabilistic record linkage from the UK Ministry of Justice's analytics team. It runs on DuckDB, Spark or Postgres.
- What to borrow: its blocking rules and match weights for merging duplicate people, customers and products, before or alongside any LLM matching.
- Maturity: about 2.5k stars, MIT, v5.0.0 in September.
- Best for: Architects and Devs.
- Rebrand watch: most "LLM entity resolution" is classic record linkage under a new name, so start here.

## Sources

- [langextract](https://github.com/google/langextract)
- [cognee](https://github.com/topoteretes/cognee)
- [splink](https://github.com/moj-analytical-services/splink)