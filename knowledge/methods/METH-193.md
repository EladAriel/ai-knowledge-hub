# METH-193: Agent memory is an attack surface: provenance, an audit screen, and DriftGuard (Adopt)

## Summary

Microsoft showed, in a lab, a phishing attack on Copilot CLI that uses device-code login. The user approves, on the real GitHub site, a code the attacker started. From that moment the attacker can steer an active session, plant false memories, and read synced sessions. Turning memory off does not delete records that were already planted. This is a lab demonstration, not an attack seen in the wild. DriftGuard detects, in real time, a memory that was pulled and is steering the agent off course, by running ahead-of-time checks of what would have happened without that memory. DriftGuard's numbers are the authors' only. Recommendation: Adopt, meaning keep a source and a time on every memory record, and add an audit screen so a user can see and delete records. Effort: medium.

## Details

From the Nov 20 methods digest. Sources: [Microsoft Security blog](https://www.microsoft.com/en-us/security/blog/2026/11/17/the-risks-of-device-code-authentication-for-ai-coding-agents/) · [DriftGuard](https://arxiv.org/abs/2611.25583).

Why it matters: every product with lasting memory is exposed to this.

## Sources

- [Microsoft: device-code phishing against coding agents](https://www.microsoft.com/en-us/security/blog/2026/11/17/the-risks-of-device-code-authentication-for-ai-coding-agents/)
- [DriftGuard](https://arxiv.org/abs/2611.25583)
