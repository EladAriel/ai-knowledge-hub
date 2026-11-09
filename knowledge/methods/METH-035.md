# METH-035: Silent cue loss in document ingestion

## Summary

Converters drop highlight/colour marks on key requirements: F1 0.690 with formatting vs 0.150 after docling and 0.075 as plain text.

## Content

**1. [Silent Cue Loss in enterprise document ingestion](https://arxiv.org/abs/2610.30026)** (arXiv, Oct 22)
- Authors often mark key requirements with highlight or color, and mainstream document converters drop those marks.
- The authors tested 76 policy documents and measured how well the model recovers the flagged requirements, scored as F1 (0 to 1). It got 0.690 with formatting kept, 0.150 after docling and 0.075 as plain text. Highlight and color drive the gap, while bold and italic barely matter.
- In a wider sample, 32.8% of 6,460 docs use color or highlight, and 10.3% use it on an obligation. Converters also don't mark which value was replaced in Word tracked changes.
- Limitation: I couldn't find a code link yet. The paper uses Microsoft's [Office Comprehension Benchmark](https://huggingface.co/datasets/microsoft/OfficeComprehensionBenchmark).
- Adopt for:
  - *Architects:* add highlight, color and tracked changes to the ingestion data contract, and name an owner for the converter.
  - *Product:* retest policy and compliance Q&A first, since it's the most exposed.
  - *Devs:* compare converter output with the originals on 20 highlighted docs, and keep the cues as tags.

**2. [Silent Cue Loss: What the writer cues and the agent doesn't see](https://arxiv.org/abs/2610.30026)**
- **What it is:** Common document converters, such as docling or converting to plain text, lose the color and highlight in Word and PDF documents. That's why agents miss requirements that the writer has indicated, and answer confidently and mistakenly.- **Why new:** This is the first time anyone has measured this loss. No parsing benchmark checks for color.
- **Evidence:**
  - 76 real policy documents were tested, with a deterministic score calculated from the OOXML.
  - With docling, the F1 drops from 0.690 to 0.150, and the result repeats in six models.
  - 32.8% of 6,460 documents contain intentional color.
  - I did not find a code.
- **Scores:** Effectiveness 4/5, hype 1/5.
- **Fit:** High for RAG and agents working on policy and compliance documents. **low** effort: to preserve the color and the highlight as tags in the controlled nth stage of the harness for verifying biomedical claims, when the only tool is PubMed. Of the 335 PubMed IDs that models cited from memory, 327 actually exist, but only 3 of them are relevant to the claim.
- **Why new:** It shows with numbers that checking "the quote exists" doesn't really check anything. In addition, queries that the agent writes himself triple the recall.
- **Evidence:** The code, prompts and all tool calls are saved. The gap with the oracle, 17 to 24 points, is significant.
- **Scores:** Effectiveness 4/5, hype 1/5.
- **Compatibility:** Any RAG system that displays sources. **Low** effort: check that the source supports the claim, and not just that it exists.
- **Recommendation: Adopt** as a test.

## Sources

- [Silent Cue Loss](https://arxiv.org/abs/2610.30026)
- [Office Comprehension Benchmark](https://huggingface.co/datasets/microsoft/OfficeComprehensionBenchmark)
