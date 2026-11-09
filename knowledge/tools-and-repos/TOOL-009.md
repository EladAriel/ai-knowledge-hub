# TOOL-009: Repos: supermemory company-brain, memoket-kite, promptfoo

## Summary

Open-sourced Slack company brain with a good permission model; embedding-free memory engine; promptfoo llm-rubric judges in CI.

## Details

supermemoryai/company-brain (1,019 stars, Apache-2.0, Cloudflare Workers): reads only with the asker's access (public/private channel/DM scopes), writes under your own connection, teammate tools need approval; memory depends on hosted supermemory API. memoket/memoket-kite (157, Apache-2.0): chats -> typed dated facts linked to sources; questions compiled to readable JSON query plans; gets 'now' right, returns nothing if never said; LoCoMo 93.51% self-reported. promptfoo (~26k, MIT): llm-rubric assertion = YAML LLM judge, CLI + CI.

## Content

**[supermemoryai/company-brain](https://github.com/supermemoryai/company-brain)** used to be a paid "company brain" product and is now open source. It lives in Slack as a teammate, remembers decisions and owners, answers questions, and acts through MCP tools.
- What to borrow: its permission model. It reads only with the asker's access. Public channels see the shared brain, private channels add that channel's memory, and DMs add personal memory. Writes run under your own connection, and using a teammate's tool needs their approval. It can also speak up on its own.
- Maturity: 1,019 stars and 140 forks, Apache-2.0, TypeScript on Cloudflare Workers, last commit Sep 28. It has a 5-minute deploy and a local dev setup (`bun run dev`). Memory depends on the hosted supermemory API, so that's a lock-in point.
- Best for: Product, to see the shape of a real company brain, and Architects, for how it scopes permissions.

**[memoket/memoket-kite](https://github.com/memoket/memoket-kite)** is a memory engine with no embeddings. It turns chats into typed, dated facts linked to their sources. Then it compiles each question into a readable JSON query plan, such as filter, sort, take one.
- What to borrow: it gets "now" right by sorting on time, and it returns nothing when something was never said.
- Maturity: 157 stars, Apache-2.0, installs with pip, last commit Oct 12. Its 93.51% on LoCoMo, a long-conversation memory benchmark, is self-reported.
- Best for: Devs and Architects.

**[promptfoo/promptfoo](https://github.com/promptfoo/promptfoo)** is an established tool, picked to go with today's eval. Its `llm-rubric` assertion is an LLM judge you write in YAML ([docs](https://www.promptfoo.dev/docs/configuration/expected-outputs/model-graded/llm-rubric/)), and it runs from the command line and in CI.
- Maturity: about 26k stars, MIT, active today.
- Best for: Devs.

## Sources

- [company-brain](https://github.com/supermemoryai/company-brain)
- [memoket-kite](https://github.com/memoket/memoket-kite)
- [promptfoo](https://github.com/promptfoo/promptfoo)
- [docs](https://www.promptfoo.dev/docs/configuration/expected-outputs/model-graded/llm-rubric/)