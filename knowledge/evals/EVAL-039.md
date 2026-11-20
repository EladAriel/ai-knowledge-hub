# EVAL-039: Eval: permission table tests and index drift check

## Summary

Tests for your permission model, plus a check that the permissions copied into your search index still match the permission system. Under a day. Added on Nov 13.

## Details

Steps (under a day): 1. Pick 5–8 user types and about 20 documents. Include a contractor, someone who left a team, a cross-team share, an admin, and the agent's own service account. 2. Write down each expected allow or deny, plus each user's expected list of visible documents. Use an OpenFGA test file, which runs with `fga model test` and a GitHub Action, or a SpiceDB validation file. Include ListObjects expectations. 3. For each user type, compare the document IDs your search filter allows against the list the permission system returns. Any difference is drift. 4. Run it again after removing someone's access and after a group change, and record how long the drift lasts. What it catches: broken permission rules, missing deny cases, and stale permission tags in the index. The Authorization-First Retrieval paper showed that permission tags in the index break down when updates lag, as they do in real systems. Who runs it: Devs run it in CI on every model change; Architects own the table of users and documents, plus the drift alert; Product confirms the user types match real users.

Effort: under a day.

## Sources

- [OpenFGA model tests](https://openfga.dev/docs/modeling/testing)
- [SpiceDB validation testing](https://authzed.com/docs/spicedb/modeling/validation-testing-debugging)
