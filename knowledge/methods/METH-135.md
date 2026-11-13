# METH-135: Safely scaling multi-agent teams with Claude Fable 5.2

## Summary

1,000 agents on an early version of Fable 5.2 reproduced a Lean proof of Fermat's Last Theorem in 28.7 hours. They had only a shell, a Git branch each, and a shared Postgres database, with no domain-specific platform and no researcher steering. Based on a Nov 9 claude.dev post.

## Details

You get large-scale autonomy, but only inside heavy sandboxing and monitoring. The agents also misjudged difficulty: early on they called 47 of 60 statements infeasible, then proved most of them. A shared SQL database plus Git was enough for the agents to coordinate—your multi-agent app may not need a custom orchestration framework. The lead agent created 5 tables (announce, assign, notes, subtasks, landed) → it assigned crews → each helper looped: read the plan → claim a subtask → write and check the proof → open a merge request → mark the task done → post a note. The hardest statement was split into a tree of 2,418 tasks, up to 10 levels deep. Safety came in layers: a VM per agent with no network, a gateway that stamps each agent's identity, an unprivileged database role with a 5-second statement limit, a classifier on every tool call, and an offline monitor. Example: migrating 200 React components to a new design system from a Python FastAPI backend: the lead agent writes rows to a Postgres subtasks table → workers claim rows with UPDATE ... WHERE claimed_by IS NULL RETURNING id → each worker runs npm run typecheck && vitest on its own branch → it marks the row done and logs any blockers to notes. Next move: if you run parallel agents, replace ad-hoc message passing with a claimable subtasks table and a Git branch per agent. Try it? Only if you already run several agents on work that splits cleanly. Otherwise, read it as research. Tips: use shared SQL tables as an agent coordination board for claims, notes, and a done log; give each agent its own Git branch and run a separate merge job, so agents never edit the same files; send the lead periodic reminders of how much time is left, so it doesn't stop early; put statement timeouts and write caps on a shared, unprivileged database role; check each tool call with a classifier before it runs, and review the team's actions offline.

## Sources

- [Safely scaling multi-agent teams with Claude Fable 5.2](https://claude.dev/blog/safely-scaling-multi-agent-teams-with-fable-5-2/)
