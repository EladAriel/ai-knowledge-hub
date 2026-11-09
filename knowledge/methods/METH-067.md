# METH-067: 'Black October': A wave of hacks for AI development platforms, and a backdoor in the Claude Code plugin in Cursor

## Summary

According to Wiz, in October at least nine AI development platforms reported breaches, including Fireworks, Railway, Warp, OpenCode and Northflank.

## Content

### 1. "Black October": a wave of hacks for AI development platforms, and a backdoor in the Claude Code extension in Cursor
Sources: [Wiz](https://www.wiz.io/blog/black-october-for-ai-developer-platforms) · [Cursor Security Notice](https://cursor.com/blog/claude-code-extension-security-notice) · [Phorion](https://phorion.io/blog/official-claude-code-vsx-compromise/) · [Microsoft](https://www.microsoft.com/en-us/security/blog/2026/10/30/inside-malicious-claude-code-branded-cursor-extension-persistent-ssh-backdoor/)
- **What is it:**
  - According to Wiz, in October at least nine AI development platforms reported breaches, including Fireworks, Railway, Warp, OpenCode and Northflank. The attackers looked for environment variables with keys from AI vendors, then used or sold them. This is called LLMjacking.
  - Separately, on 29.10 between 11:27 and 22:35 (Israel time), the Cursor plugin market distributed versions 2.1.312 and 2.1.313 of the Claude Code plugin with malicious code. The code tried to add the attacker's SSH key, open a reverse SSH tunnel, and leave a component that continues to run even after the plugin is removed.
- **Why new:** Supply chain is a recognized risk. What's new is that Wiz connects all the events into one campaign that targets AI keys, and that there is detailed telemetry on what happens to the key after it is stolen.
- **Evidence:**
  - The first attempt to use the stolen key came about 30 minutes after the theft. The first call requested Fable 5.1, failed, and switched to Opus 5.5. Then about 800 thousand calls to Bedrock were registered for about 30 hours, all through `global.*` profiles.
  - Cursor and Phorion published identifiers and a cleanup script. According to them, a bug in the malicious code likely prevented most computers from enabling SSH, but the attacker's key and fixed component were written anyway.- **What has not been proven:** The connection between all nine events is one global memory. **medium** effort.
- **Recommendation: Pilot.** This continues the skepticism towards memory from 10.21 and 10.26.

## Breaking-change alerts
- **Backdoored Claude Code extension on Cursor's marketplace.** Versions 2.1.312 and 2.1.313 of `Anthropic.claude-code` were live on Oct 29 from about 11:27 to 22:35 (Israel time), for macOS and Windows. The extension adds an SSH key, a reverse tunnel and persistence, and it sends out the *names* of your secret env vars. Uninstalling it doesn't clean it up, so use Cursor's remediation scripts. You can check a machine with `grep -qs svc-telemetry ~/.ssh/authorized_keys`. The VS Code Marketplace and npm weren't affected. Sources: [Cursor notice](https://cursor.com/blog/claude-code-extension-security-notice), [Microsoft analysis](https://www.microsoft.com/en-us/security/blog/2026/10/30/inside-malicious-claude-code-branded-cursor-extension-persistent-ssh-backdoor/), [Phorion write-up](https://phorion.io/blog/official-claude-code-vsx-compromise/), [HN thread](https://news.ycombinator.com/item?id=50300683).

## Sources

- [Wiz](https://www.wiz.io/blog/black-october-for-ai-developer-platforms)
- [Cursor security notice](https://cursor.com/blog/claude-code-extension-security-notice)
- [Phorion](https://phorion.io/blog/offical-claude-code-vsx-compromise/)
- [Microsoft](https://www.microsoft.com/en-us/security/blog/2026/10/30/inside-malicious-claude-code-branded-cursor-extension-persistent-ssh-backdoor/)
- [DevEx Radar: HN thread (check: grep -qs svc-telemetry ~/.ssh/authorized_keys)](https://news.ycombinator.com/item?id=50300683)
