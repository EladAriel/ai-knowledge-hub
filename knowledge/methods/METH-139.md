# METH-139: Gemini Decisions API (Gemini Decision 1): closed decisions with probabilities and confidence

## Summary

A new Google endpoint for closed decisions: yes or no, a choice from up to 255 options, and a score against a rubric. You can ask up to 1,000 questions on a shared input in one call, and the reply includes probabilities and a confidence score.

## Details

The idea is not new. This is the third player in the decision-model category, after Jev and OpenAI. What sets it apart is that it is fully multimodal (video, audio, PDF) and that it does not charge for output tokens. Evidence: it is generally available, with docs and an SDK. Simon Willison tested it himself on video and got reasonable probabilities: 0.92 for 'robot' and 0.05 for 'dragon'. Google claims 150 to 250 milliseconds and good calibration, but has not published a calibration comparison against Jev or OpenAI. Scores: effectiveness 4/5, hype 2/5. Fit: high for any agent product—routing, tool choice, policy checks, ranking context, and a gate before escalating to a person. Effort: low. Recommendation: Pilot. Place it against Jev and GPT-6 Luna on a real set of your own decisions, and measure calibration, not only accuracy. Recurring theme: decision models appeared here on Oct 10, Nov 7, Nov 9 (Flide) and Nov 10 (Strands Decider).

## Sources

- [Gemini Decisions API](https://blog.google/innovation-and-ai/technology/developers-tools/gemini-decisions-api/)
- [Simon Willison](https://simonwillison.net/)
