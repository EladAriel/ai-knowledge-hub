# DEVX-058: Mod: honest /copy that prefixes the clipboard with the session model (Claude Code command.run hook)

## Summary

A Claude Code mod that intercepts the /copy command so the copied text starts with 'Via `\<model>`:' and is wrapped in a markdown fence, so anyone reading pasted agent text in chat or tickets sees its source. Keeps the /copy muscle memory.

## Details

By Jamie Tanna (blog post Nov 3, CC-BY-NC-SA-4.0). Registers on("command.run", { command: "copy" }), takes an optional N (1 = latest assistant reply), reads $.session.messages() and $.session.model(), builds 'Via `\<model>`:' + a five-backtick markdown fence around the reply, and calls $.ui.copy. The post does not name the on-disk mods path; place it as a Claude Code mod that exports register. Full TypeScript is in the source text.

## Sources

- [Honest Claude (jvt.me)](https://www.jvt.me/posts/2026/11/03/honest-claude-meatproxy)
