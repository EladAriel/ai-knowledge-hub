# METH-013: OAR: Ownership-Aware Routing

## Summary

When the tables in the organization belong to different owners, you have to choose how to send the query.

## Content

### 2. [OAR: Ownership-Aware Routing](https://arxiv.org/abs/2610.18157)
- **What is it:** When the tables in the organization belong to different owners, you have to choose how to send the query. Sending at the same time to all owners (fan-out) succeeds in questions concerning one owner, and crashes when it is necessary to join between different owners (up to 4.3% success). Transfer in a chain between owners (relay) behaves in the opposite way. OAR writes a SQL draft on public consent only, counts how many owners are involved, and chooses the path before touching private data.
- **Why new:** The decision is based on who owns the data, and not only on the complexity of the query as in Adaptive-RAG.
- **Evidence:** Tested in 13 settings, on PeopleJoin and BIRD, with 3 model families. The results do not fall significantly short of the best fixed protocol. In organizations that were not seen in the development there is an improvement of up to 9.3 points.
- **Scores:** Effectiveness 4/5, hype 1/5.
- **Suitability:** Very high for organizational assistants with many departments and private requirements. **low to moderate** effort.
- **Recommendation: Adopt**

## Sources

- [OAR: Ownership-Aware Routing](https://arxiv.org/abs/2610.18157)
