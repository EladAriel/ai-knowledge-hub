# METH-001: Sonnet 5.5 migration (thinking default, effort recalibrated)

## Summary

Smarter than Sonnet 5, ~30% faster, same price; up to 30% cheaper per task; breaking API changes.

## Content

- Sonnet 5.5 is smarter than Sonnet 5 and about 30% faster, at the same per-token price ($2 in and $10 out per million tokens). It usually costs up to 30% less per task because it needs fewer tokens. The trade-off is that Opus 5.5 is still the better pick for long, judgment-heavy work, and the upgrade includes breaking API changes.

- It's the model to reach for on well-scoped coding, bug fixes, quick feature work and agent tasks you run over and over, which covers most of the Claude calls an app makes.

- Thinking is on by default, so a response can start with a thinking block. `thinking: {"type": "disabled"}` and forced `tool_choice` now return 400 errors, so use `between_tools` (low to high effort only) and `tool_choice: auto` with `strict: true` tools instead.

- Effort levels have been recalibrated, so your old settings won't behave the same. Use medium for agent work, low or medium for chat, and xhigh or max only if your evals show a gain. You also get a native 1M-token context window, up to 128k tokens of output, and caching for prompts as short as 512 tokens.

- Next move: in Claude Code, run `/claude-api migrate this project to claude-sonnet-5-5`. Then re-run your effort comparison and remove old Sonnet 5 workarounds.

- Should you try it? Yes for well-scoped app features and repeated agent tasks. For long-horizon work, only if your evals hold up, since Opus is still the default there.

Example
A FastAPI chat endpoint with a React frontend.
Change the model to `claude-sonnet-5-5` → replace `content[0].text` with a loop that reads each block by type → set `output_config={"effort": "medium"}` → switch forced `tool_choice` to `auto`, with `strict: True` and `additionalProperties: False` on the tool → the React UI shows `display: "summarized"` thinking blocks as progress notes.

- Bug fixes and quick feature work in Claude Code with `/model sonnet`.
- Polished documents, slides and spreadsheet cleanup where an eye for design helps.
- Repeated agent tasks like investigation, review and drafting.
- Cheaper caching of short system prompts and tool definitions.

[Building with Claude Sonnet 5.5](https://claude.dev/blog/building-with-claude-sonnet-5-5/)

## Sources

- [Building with Claude Sonnet 5.5](https://claude.dev/blog/building-with-claude-sonnet-5-5/)
