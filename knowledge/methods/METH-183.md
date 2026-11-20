# METH-183: Using a chaos loop to harden the Claude Docs launch

## Summary

A long-running Claude Code session hammered staging for two weeks, breaking things on purpose and fixing whatever fell over. Claude Docs then served 4.6M docs and 2B requests with 60 errors, but the loop cost about $125k in inference (the author's rough estimate for a small service is $3k to $10k). Try it only if you have a real launch or traffic spike coming. For everyday apps, the verification post (DEVX-093) is the cheaper win.

## Details

The real lesson for app builders, from the Nov 17 claude.dev post, is legibility: Claude can only fix what your telemetry can explain. Write down your invariants and approval rules first, and newer models can hold a goal for weeks.

Flow: pick a scenario → saturate it → Claude reads telemetry through an MCP server → proposes fixes → ships the ones that are easy to undo and reruns → stops and asks you about hard-to-undo ones like schema changes. Every query logged rows scanned versus rows returned, so slow queries were easy to spot.

Practical one-liners: paranoid scenarios included 10M docs in a day, 22k reconnects at once, and one hot doc with hundreds of viewers; Claude adds missing telemetry on every iteration instead of waiting for an outage; prefer stacks and dependencies Claude can measure, and vendor the few libraries you really need; risky fixes ship behind runtime flags, so a problem in production becomes a flag flip.

The Nov 16 verification post on the same site is covered in DEVX-093 (a recorded `verify` skill, plus property and differential tests).

## Sources

- [Chaos loop (Claude Docs launch)](https://claude.dev/blog/chaos-loop-claude-docs-launch/)
