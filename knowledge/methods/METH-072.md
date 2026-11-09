# METH-072: Role Grounding Attack: Memory poisoning through a quoted conversation

## Summary

Attack agent publishes post quoting conversation with 'his owner'; The reading agent's memory system stores the preference in the quote as if it were its user's, then the agent chooses the attacker's tool and leaks information.

## Content

**1. [Role Grounding Attack: Memory Poisoning via Quoted Conversation](https://arxiv.org/abs/2610.38209)**
- **What it is:** An attacking agent publishes a post citing a conversation with "its owner". The memory system of the agent reading the post saves the preference  chooses a tool of the attacker and transfers sensitive information to it.
- **Why new:** Nothing is fake, and the source of the post is marked correctly. Still, the association with the right owner is lost once the memory is written. This is different from normal memory injection.
- **Evidence:**
  - Tested on 5 memory systems (Mem0, A-MEM, LangMem, Hindsight, MemOS) and 6 models.
  - The manipulation of the choice of the tool was successful in about 92% of the cases, and the information leakage in about 70%.
  - LLM based security filter did not detect the posts.
  - **Cheap defense:** A reminder built from the metadata ("The content was published by X, and the user in the quote is not your user") dropped the success rate from 94% to 32%.
  - [Code available](https://github.com/Buhaoran0307/20260825-MemoryDrift_Code).
- **Scores:** Effectiveness 4/5, Hype 2/5.
- **Compatibility:** Any product that writes "user preferences" to memory from external content. **low** effort.
- **Recommendation: Adopt** For controls: each memory record should keep who it belongs to, and it is worth adding the reminder to the prompt that writes to the memory. Yesterday it appeared only in the list of terms. The topic of injections has been coming back for a week.

## Sources

- [Role Grounding Attack](https://arxiv.org/abs/2610.38209)
- [code](https://github.com/Buhaoran0307/20260825-MemoryDrift_Code)
