# EVAL-030: Eval: duplicate crowding and repeat syncs

## Summary

Checks that copies of the same document (Drive, Confluence, an email attachment) don't take several top results, and that running a sync twice creates no extra copies. Under a day; becomes a CI test.

## Details

Steps (under a day):
1. Hash the cleaned-up text of every chunk to find exact duplicates.
2. Use MinHash or embedding similarity above 0.95 to find near-duplicates.
3. Report the duplicate rate for each source.
4. Run your golden set and flag every question where two or more of the top results are copies of the same content.
5. Keep only the most authoritative or newest copy, then rerun recall@k.
6. Run the same sync twice; chunk count and IDs must stay the same. Make this a CI test.
Catches: wasted context and copies that look like several sources agreeing; old copies ranking above current ones; connectors that re-add the same content on every sync.
Who runs it: Devs in CI; Architects decide what counts as a duplicate and which source wins; Product reviews questions where duplicates pushed out the right answer.

## Content

## Simple eval technique: duplicate crowding and repeat syncs

**What it is:** this checks two things. First, that copies of the same document, say in Drive, Confluence and an email attachment, aren't taking up several of your top results. Second, that running a sync twice doesn't create extra copies.

**Steps (under a day):**
1. Hash the cleaned-up text of every chunk to find exact duplicates.
2. Use MinHash or embedding similarity above 0.95 to find near-duplicates.
3. Report the duplicate rate for each source.
4. Run your golden set and flag every question where two or more of the top results are copies of the same content.
5. Keep only the most authoritative or newest copy, then rerun recall@k.
6. Run the same sync twice. The chunk count and IDs must stay the same. Make this a CI test.

**What it catches:**
- Wasted context, and copies that look like several sources agreeing.
- Old copies ranking above current ones.
- Connectors that add the same content again on every sync.

**Who runs it:**
- *Devs* run it in CI.
- *Architects* decide what counts as a duplicate and which source wins.
- *Product* reviews the questions where duplicates pushed out the right answer.

## Sources

- No external source link (in-house technique note).
