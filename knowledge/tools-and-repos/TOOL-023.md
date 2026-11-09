# TOOL-023: Cursor Agent SDK (GA), local trial only

## Summary

It lets you define agents as code, with built-in evals and a 'security-reviewer' template. Effort: ~45 min for a local trial with no deploy.

## Content

### 4. Cursor Agent SDK (GA), local trial only — Enterprise feasibility: Medium | Stage: Assess
- **What changed:** Cursor's [Agent SDK](https://cursor.com/changelog/agent-sdk) is generally available. It lets you define agents as code, with built-in evals and a `security-reviewer` template.
- **Effort:** ~45 min for a local trial with no deploy.
- **Watch the package name:** the changelog says `@cursor/agent-sdk`, which doesn't exist on npm. Install only the name from the docs, [@grok/agent-sdk](https://www.npmjs.com/package/@grok/agent-sdk), to avoid a typo-squatted package. It's proprietary, so get a security review before any hosted deploy.
- **PoC:**
```bash
npm i -g @grok/agent-sdk && agent-sdk login
agent-sdk init ./security-reviewer --template security-reviewer --var repos=acme/api
agent-sdk eval
```
- **Success metric:** Review-agent findings per PR compared with human review.

## Sources

- [Agent SDK](https://cursor.com/changelog/agent-sdk)
- [npm package](https://www.npmjs.com/package/@grok/agent-sdk)
