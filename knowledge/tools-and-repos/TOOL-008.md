# TOOL-008: Scan third-party skills and plugins with NVIDIA SkillSpector

## Summary

SkillSpector v2.13.0 shipped Oct 16; claude-code-templates now shows a SkillSpector result on every catalog component.

## Details

Their scan of 1,890 components flagged 82 as CRITICAL and 61 as HIGH (PR #1204).

## Content

## 3. Scan third-party skills and plugins with NVIDIA SkillSpector: Enterprise feasibility High | Stage Trial
- **What changed:** [v2.13.0](https://github.com/NVIDIA/SkillSpector/releases/tag/v2.13.0) shipped Oct 16. As of Oct 18, claude-code-templates shows a SkillSpector result on every component in its catalog. Their scan of 1,890 components flagged 82 as CRITICAL and 61 as HIGH ([PR #1204](https://github.com/davila7/claude-code-templates/pull/1204)).
- **How it works:** a static scan with no AI calls checks a skill folder for prompt injection, data exfiltration, MCP over-permission and tool poisoning. It writes SARIF (the standard format code-scanning tools import) and exits with 1 when the risk is high. It needs no API key, so it also works in air-gapped setups.
- **Effort:** ~15 min.
- **PoC:**
```bash
uv tool install git+https://github.com/NVIDIA/SkillSpector.git@v2.13.0
skillspector scan ./skills/some-skill/ --no-llm --format sarif --output skill.sarif
```
- **Success metric:** every skill or plugin on your internal allowlist has a scan report, and no HIGH or CRITICAL finding is accepted without a named reviewer.
- **Project health:** NVIDIA, Apache-2.0, about 20k stars, commits within the last few days. It's noisy on pentest-style skills.
- **Sources:** [SkillSpector](https://github.com/NVIDIA/SkillSpector), [NVIDIA docs](https://docs.nvidia.com/skills/scanning-agent-skills), [Microsoft APM scanners](https://microsoft.github.io/apm/integrations/external-scanners/) (seen in 4 sources)

## Sources

- [v2.13.0](https://github.com/NVIDIA/SkillSpector/releases/tag/v2.13.0)
- [PR #1204](https://github.com/davila7/claude-code-templates/pull/1204)
- [SkillSpector](https://github.com/NVIDIA/SkillSpector)
- [NVIDIA docs](https://docs.nvidia.com/skills/scanning-agent-skills)
- [Microsoft APM scanners](https://microsoft.github.io/apm/integrations/external-scanners/)