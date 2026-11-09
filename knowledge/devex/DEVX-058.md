# DEVX-058: Mod: honest /copy that prefixes the clipboard with the session model (Claude Code command.run hook)

## Summary

A Claude Code mod that intercepts the /copy command so the copied text starts with 'Via `\<model>`:' and is wrapped in a markdown fence, so anyone reading pasted agent text in chat or tickets sees its source. Keeps the /copy muscle memory.

## Details

By Jamie Tanna (blog post Nov 3, CC-BY-NC-SA-4.0). Registers on("command.run", { command: "copy" }), takes an optional N (1 = latest assistant reply), reads $.session.messages() and $.session.model(), builds 'Via `\<model>`:' + a five-backtick markdown fence around the reply, and calls $.ui.copy. The post does not name the on-disk mods path; place it as a Claude Code mod that exports register. Full TypeScript is in the source text.

## Content

**[Honest `/copy` model attribution](https://www.jvt.me/posts/2026/11/03/honest-claude-meatproxy/)** intercepts `command.run` for `/copy` so the clipboard starts with `Via \`<model>\`:` and a markdown fence. Keeps the `/copy` muscle memory. Jamie Tanna, CC-BY-NC-SA-4.0. Effort: ~10 min.
```ts
import type { Register } from "claude-code";

export const register: Register = (on) => {
  on("command.run", { command: "copy" }, async ($, e) => {
    const arg = e.args.trim();
    const n = arg === "" ? 1 : Number(arg);
    if (!Number.isInteger(n) || n < 1) {
      return { text: `Usage: /copy [N] where N is 1 (latest), 2, 3, … Got: ${arg}` };
    }
    const messages = await $.session.messages();
    const replies = messages.filter((m) => m.role === "assistant" && m.text !== "");
    const reply = replies.at(-n);
    if (reply === undefined) {
      return { text: `No assistant response #${n} to copy.` };
    }
    const model = await $.session.model();
    const text = ["Via `" + model + "`:", "", "

```

## Sources

- [Honest Claude (jvt.me)](https://www.jvt.me/posts/2026/11/03/honest-claude-meatproxy)
- [Honest `/copy` model attribution](https://www.jvt.me/posts/2026/11/03/honest-claude-meatproxy/)