# METH-141: DocFS: documents as a filesystem for the agent

## Summary

Converts long, multimodal documents into a folder tree that mirrors the section structure, with links between the text, tables and figures. The agent navigates with ordinary filesystem tools: search, moving between folders, and reading. arXiv 2611.12957.

## Details

What's new: mostly a rebrand, because the idea of files instead of RAG already appeared (DKGI, Oct 15, METH-014). The new part is applying it to questions about multimodal documents, with an explicit match between the information structure and the tools that work on it. Evidence: the authors report a leading result on MMLongBench-Doc (+2.9) and FinRAGBench-V (+4.3), and up to 10 times fewer tokens and less time. Not independently reproduced, and no repo was found. Scores: effectiveness 3/5, hype 2/5. Fit: good for enterprise knowledge systems with long documents such as contracts, reports and technical documents. Effort: medium. Recommendation: Pilot, as a comparison against the chunking you do today.

## Sources

- [DocFS (arXiv)](https://arxiv.org/abs/2611.12957)
