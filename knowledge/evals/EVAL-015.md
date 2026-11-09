# EVAL-015: Eval: canary freshness and coverage test

## Summary

Plant tagged test changes in real sources and time how long each takes to appear or disappear in search.

## Details

1) Sandbox in 2-3 sources with users A and B (B loses access later). 2) Canaries with unique tokens (CNRY-7f3a): new doc, v1->v2 edit, delete, revoke B, attachment, highlighted requirement (+ injection string). 3) Every 5-15 min search as A and B by token and natural question. 4) Log time-to-searchable p50/p95, docs missing after target, zombie docs, stale versions, revoked-access lag incl. cached answers. 5) Run daily, alert on misses.

## Content

## Simple eval technique: canary freshness and coverage test

**What it is:** you plant tagged test changes in your real sources, then time how long each one takes to show up, or disappear, in your search results.

**Steps (under a day):**
1. Set up a sandbox in 2–3 sources with two test users: user A, and user B who will lose access later.
2. Plant canaries with unique tokens (like `CNRY-7f3a`) and record the time each was planted. Use six kinds: a new doc, an edit from v1 to v2, a delete, revoking B's access, an attachment, and a highlighted requirement. You can also add an injection string.
3. Every 5–15 minutes, search as A and as B. Use the exact token and also one natural question per canary.
4. Log five things:
   - Time until each change is searchable, as the median and 95th percentile.
   - Docs still missing after the target window.
   - Deleted docs that still show up, and for how long.
   - Old versions still being returned.
   - How long B keeps seeing the revoked doc, including in cached answers.
5. Run it daily and alert when a target is missed.

**What it catches:** missed webhooks, expired delta tokens, a sync that stopped picking up changes, cleanup that silently stopped, folder permissions that never synced, stale caches, and dropped highlights.

**Who runs it:** Devs run it in CI or on a schedule. Product owns the thresholds and the weekly trend. Architects own the test users and the targets for each source.