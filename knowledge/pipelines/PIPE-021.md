# PIPE-021: Pipeline: permissions for derived knowledge and agent identity

## Summary

sync permissions  -> permission filter in the index -> live recheck of top results at the source -> redact sensitive fields -> audit log.

## Details

Search as the user, not the agent: an agent searching as itself returns whatever the agent can see; AWS says its own permission filtering isn't true authorization, the app must verify the user and pass their identity (QueryNow guide). Synced permissions go stale between syncs, so recheck the final top results live at the source (AWS two-step check in Bedrock and Quick). Sensitivity labels travel with content: Azure AI Search checks Purview labels and SharePoint permissions at query time with the user's Microsoft sign-in token. A summary of 5 docs is visible only to people who can see all 5 (ACL intersection): store source_ids on every derived item, recompute access when any source changes, don't index anything you can't trace to its sources. Default to private: a chunk with no permission data is private. Owners: Architects own the data contract (every item carries acl, label, source_ids, derived_from), identity pass-through and private-by-default; Product decides which sources open company-wide first and tracks how often permissions block an answer; Devs build one shared retrieval wrapper (rest of this part was cut off in the transcript). Terms: security trimming, on-behalf-of identity, ACL intersection. Recurring theme: authorization outside the model has come up 7 times, focus now on derived items.

## Content

## Pipeline pattern of the day: permissions for derived knowledge and agent identity

sync permissions  -> filter by permissions in the index -> recheck the top results live at the source -> redact sensitive fields -> write an audit log

- **Search as the user, not as the agent.** An agent searching as itself returns whatever the agent can see. AWS says its own permission filtering isn't true authorization: your app has to verify the user and pass their identity ([QueryNow guide](https://www.querynow.com/ai-agents/knowledge/permission-aware-retrieval)).
- **Synced permissions go stale between syncs,** so recheck the final top results live at the source. AWS uses this two-step check in Bedrock and Quick.
- **Sensitivity labels travel with the content.** [Azure AI Search](https://learn.microsoft.com/en-us/azure/search/search-document-level-access-overview) checks Purview labels and SharePoint permissions at query time, using the user's Microsoft sign-in token.
- **A summary of 5 docs is visible only to people who can see all 5.** Store `source_ids` on every derived item, and recompute its access when any source changes. Don't index anything you can't trace back to its sources.
- **Default to private.** A chunk with no permission data is private, never public.
- **Who owns it:**
  - *Architects* own the data contract: every item carries `acl`, `label`, `source_ids` and `derived_from`. They also own passing the user's identity through to every search, and the private-by-default rule.
  - *Product* decides which sources open to the whole company first and which stay team-only. It also tracks how often permissions block an answer, so users understand why answers are missing.
  - *Devs* build one shared retrieval wrapper that cha...nswer sits in one known doc.
2. Copy each doc and change the key fact to a believable fake value, like a different date, number or owner.
3. Run each question with the edited doc in the context, or in a temporary index.
4. Score with code: the answer passes if it has the fake value and fails if it has the original.
5. **Conflict version:** put the old and new doc side by side, with only one marked current, and count how often the wrong one wins. Insight 2 suggests this will be your worst case.

**What it catches:** the model ignoring the retrieved doc, stale summaries or memories winning over fresh docs, cache hits after a source was edited, and version conflicts.

**Who runs it:** Devs build it and run it in CI on every prompt, model or cache change. Product picks the questions that matter most to users. Architects set the pass bar as a release gate, for example at least 95% of answers following the doc.

## Sources

- [QueryNow: permission-aware retrieval](https://www.querynow.com/ai-agents/knowledge/permission-aware-retrieval)
- [Azure AI Search document-level access](https://learn.microsoft.com/en-us/azure/search/search-document-level-access-overview)