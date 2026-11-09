# TOOL-029: Repos: openwiki, TencentDB-Agent-Memory, OpenViking

## Summary

Compile repos/docs into a source-linked wiki (CLI + MCP); shared team memory hub; virtual file system with L0/L1/L2 detail levels.

## Details

langchain-ai/openwiki (~17.6k, MIT, npm i -g openwiki; works in Claude Code/Cursor/Codex): claim source hashes, model-free search/read tools, linked multi-repo workspaces. TencentCloud/TencentDB-Agent-Memory (~30k, MIT): proxy via API base URL; private/team/restricted visibility per user/role/agent; review before a personal skill becomes a team skill. volcengine/OpenViking (~41k, AGPL-3.0): viking:// folders with L0 summary/L1 overview/L2 full; folder-scoped search; warns against RAG evals for memory.

## Content

**[TencentCloud/TencentDB-Agent-Memory](https://github.com/TencentCloud/TencentDB-Agent-Memory)** is a shared memory hub for a team. It turns chats into memories and skills, docs into a wiki, and code into a code graph. Agents connect by pointing their API base URL at its proxy.
- What to borrow: private, team and restricted visibility controlled per user, role and agent, plus a review step before one person's skill becomes a team skill.
- Maturity: about 30k stars and 2.9k forks, last push Oct 28, MIT license, TypeScript. It starts with one script, `start-all.sh`. Its only benchmark is its own PersonaMem result, which went from 48% to 76%.
- Best for: Architects, as a reference for governance.

**[volcengine/OpenViking](https://github.com/volcengine/OpenViking)** stores knowledge, memory and skills in one virtual file system (`viking://`). Each folder has three levels of detail:
  - L0, a one-line summary.
  - L1, an overview.
  - L2, the full content, loaded only when needed.
- What to borrow: search scoped to one folder instead of a single flat index, and summaries the agent reads before opening the source. Its benchmark guide also warns against using RAG evals to measure memory.
- Maturity: about 41k stars and 3.3k forks, pushed today, with Python, Go and TypeScript SDKs. The benchmarks are its own.
- License: AGPL-3.0, so check with legal before building it into your product.
- Best for: Devs and Architects.

## Sources

- [openwiki](https://github.com/langchain-ai/openwiki)
- [TencentDB-Agent-Memory](https://github.com/TencentCloud/TencentDB-Agent-Memory)
- [OpenViking](https://github.com/volcengine/OpenViking)