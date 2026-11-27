# TOOL-052: Mastra Knowledge: a company knowledge base the agent can also edit, in TypeScript

## Summary

RAG only reads, so when facts change someone has to update them by hand. Mastra Knowledge stores knowledge as markdown pages, each shared with the whole company, one user, or one conversation. The agent gets 5 tools: search, list, read, edit a page, and add a note. It ships in @mastra/core 1.82 and later. Importers for Notion, Confluence, Linear and Zendesk are promised for the next release.

## Details

Reported Nov 20. Why it matters: it fits a TypeScript stack, and those three sharing levels give you basic access control for free.

Next step: prototype one company-wide space and watch what the agent writes back. For: devs and product.

## Sources

- [Mastra Knowledge](https://mastra.ai/blog/introducing-knowledge)
