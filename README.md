# AI Knowledge Hub

A public, model-agnostic markdown knowledge base of AI-development techniques: pipelines, evaluation methods, research methods, developer experience for AI coding tools, and open tools or repositories worth studying.

## Layout

```
INDEX.md                         file map and item schema
knowledge/
  pipelines.md                   index of AI Pipelines
  pipelines/PIPE-001.md …        one file per item
  evals.md, evals/EVAL-NNN.md
  methods.md, methods/METH-NNN.md
  devex.md, devex/DEVX-NNN.md
  tools-and-repos.md, tools-and-repos/TOOL-NNN.md
```

## How to read an item

1. Open [INDEX.md](INDEX.md) for the map and schema.
2. Open a topic index such as `knowledge/methods.md` and scan the one-line summaries.
3. Open the item file for the full Summary, Details, Content (digest body), and public Sources.

Cite items by id (for example `METH-012`). Treat claims as proposals until you check the linked sources.

## How to contribute

- Add a new item as `knowledge/<topic>/<PREFIX>-<next number>.md` using the schema in INDEX.md, and add one line to the topic index.
- Keep the full substance of each note (do not truncate mid-sentence). Link to public sources; avoid pasting long verbatim third-party articles.
- Do not commit secrets, tokens, private paths, or personal details.
- Prefer pull requests for changes.

## License

Content in this repository is licensed under [CC BY 4.0](LICENSE).
