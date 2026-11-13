# METH-130: CLADE: vague evidence makes models guess

## Summary

When a passage only names a broad category but the question asks about a specific item, models answer instead of saying "I don't know." For example, the passage says "hyperlipidemia" and the question asks about "familial hyperlipidemia." Declining to answer drops 13.8 points, and about half of those guesses are wrong.

## Details

What does not fix it: lowering the confidence threshold, a bigger model, or telling it to decline when unsure. What helps: looking up the category in an ontology. Once the right category is known, the true answer is in its list of sub-items 98.5% of the time. Still, the full pipeline only goes from 10.0% to 26.8% correct, so the problem is not solved. Why it matters: in a company knowledge base, phrases like "the platform team" or "Q3 contracts" are often the only evidence you have. Your hierarchy of entities is what narrows them to a short list. Effort: medium. Adopt for: Architects—make parent-child category links a required part of the ontology; Product—count "answered from vague evidence" as a failure, not a success; Devs—add a step that spots a category word, looks up what's under it, then either asks the user or searches again. arXiv 2611.14355.

## Sources

- [CLADE (arXiv)](https://arxiv.org/abs/2611.14355)
