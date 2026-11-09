# DEVX-001: Claude Code mods (plugin JS/TS middleware)

## Summary

Small JS/TS files inside plugins that hook session events, rewrite or block actions, and draw terminal UI; full access, API may change.

## Content

- Mods are small JS or TS files that ship inside Claude Code plugins. They hook session events, can rewrite or block what Claude Code does, and can draw their own terminal UI. The trade-off is power versus trust: a mod runs with Claude Code's full access, and the API can change between releases.

- For a React, Python and TypeScript builder, this is a way to put your app's conventions and guardrails into every session so you don't have to repeat them in prompts.

- Each mod exports `register(on)`, and every hook gets `$` (the mods API), the event `e`, and `next`. Calling `next(e)` passes the event along, `next({ ...e, changed })` rewrites it, and returning `{ deny }` refuses it, much like middleware.

- Keep data in `$.state` so it survives hot reload. Check your work with `claude plugin validate` and test it against the real runtime with `claude plugin test`. You need Claude Code 2.1.287 or later.

- Next move: run `claude`, describe the mod you want in plain words, and allow hot reload. To keep the mod, copy its folder out and install it from a marketplace.

- Should you try it? Yes. Start with a mod that only watches before you build one that blocks or rewrites.

Example
A `prompt.submit` mod for your React + TypeScript frontend and FastAPI backend that adds your repo's `CONVENTIONS.md` to every prompt.
You type "add a settings page" → the hook reads `CONVENTIONS.md` with `$.fs.read` (React function components, TanStack Query, Zod schemas in `src/schemas/`, Pydantic models on FastAPI routes, Vitest and pytest) → it appends that text to the prompt and calls `next` → Claude builds a page that already fits your stack.

- Token Weather shows how full the context window is, in a band above the prompt.
- Blast Radius holds `rm -rf`, `git reset --hard` and migrations until you press Proceed or Cancel.
- Replay Theater steps through the last turn's edits one diff at a time with `/replay`.
- Other ideas from the article: a cost meter, a pane listing the files Claude has read, or a toast when a long turn finishes.

[Getting started with Claude Code mods](https://claude.dev/blog/getting-started-with-claude-code-mods/)

## Sources

- [Getting started with Claude Code mods](https://claude.dev/blog/getting-started-with-claude-code-mods/)
