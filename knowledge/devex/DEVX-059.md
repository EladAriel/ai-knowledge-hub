# DEVX-059: Rotate secrets leaked via .claude/settings.local.json ('Yes, and don't ask again') and stop tracking the file

## Summary

Apiiro found 104,185 public copies of .claude/settings.local.json; 1,122 (about 1.1%) held at least one secret, because 'Yes, and don't ask again' writes the approved Bash command verbatim as an allow rule and the gitignore protection is only a per-user global exclude. Search the org, rotate every secret the file ever held, untrack it and add **/.claude/settings.local.json to every repo .gitignore.

## Details

Mechanism: the allow rule is the command string itself; Claude Code adds **/.claude/settings.local.json only to the user's global git excludes, which do not travel with the project, a later git init, or another clone. Shared .claude/settings.json can hold the same secrets; deleting the file does not clean history, forks, images or archives. Numbers (THN summarizing Apiiro, reported Nov 7): 1,379 distinct secrets in current copies incl. 379 DB passwords, 43 SSH logins, 42 GitHub/GitLab/npm tokens, 23 AWS keys, across 63 orgs; counting history, shared settings.json (298 of 76,011) and saved agent chat logs, 2,539 secrets in 1,994 repos. In 539 of 1,105 leaking repos a Claude-coauthored commit changed the file. gitleaks flagged 564/1,122, TruffleHog 643/1,122, 215 missed by both (passwords after PGPASSWORD=, sshpass -p, mysql -p). Of 16 coding agents compared, only Claude Code saved the full approved command in a project file by default.
PoC: search org + history for filename:.claude/settings.local.json OR filename:.claude/settings.json; rotate first; git rm --cached .claude/settings.local.json; add **/.claude/settings.local.json to .gitignore (official pattern from the settings docs); prefer patterns like Bash(npm run:*) and $VARS over literal secrets.
Success metric: no newly committed settings.local.json; every credential that appeared has been rotated; every active repo .gitignore has the pattern.
Org challenge: the per-user exclude does not travel; common scanners miss command-embedded passwords.
Feasibility High, stage Adopt; seen in 6 sources. Includes the related breaking-change alert and the 'Add **/.claude/settings.local.json to every repo .gitignore' ready-to-use mod (~10 min).

## Content

- **“Yes, and don’t ask again” saved secrets into 1,122 public `.claude/settings.local.json` files on GitHub (Apiiro, reported Nov 7).** Choosing that option writes the approved Bash command, verbatim, as an allow rule. Claude Code then adds `**/.claude/settings.local.json` only to that user’s global git excludes, not the repo `.gitignore`, so the protection does not travel. [The Hacker News](https://thehackernews.com/2026/11/claude-codes-dont-ask-again-file.html) summarizing Apiiro: 104,185 public copies in 103,617 repositories; 1,122 copies (about 1.1%) held at least one secret (1,379 distinct secrets in current copies), including 379 database passwords, 43 SSH logins, 42 GitHub/GitLab/npm tokens and 23 AWS keys, across 63 organizations. One notified company confirmed a key had been live. Older history held 734 more secrets in 509 repos; counting history, shared `.claude/settings.json` (298 of 76,011 public copies), and saved agent chat logs, the total given is 2,539 secrets in 1,994 repositories. Rotate first, then untrack and gitignore.

### 1. Search the GitHub org for `.claude/settings.local.json`, rotate every secret those files ever held, then stop tracking the file — Enterprise feasibility: High | Stage: Adopt
- **What changed:** new this lookback. Apiiro’s November 5 findings were written up Nov 7; [HN discussion](https://news.ycombinator.com/item?id=50407882). Official [settings docs](https://code.claude.com/docs/en/settings) still describe the same write path and per-machine global exclude. Of 16 coding agents Apiiro compared, Claude Code was the only one confirmed to save the full approved command in a project file by default.
- **How it works:** the allow rule is the command string itself. Global git excludes do not travel with the project, a later `git init`, or another clone. Shared `.claude/settings.json` can hold the same secrets. Deleting the file does not clean history, forks, images, or archives. In 539 of 1,105 leaking repositories a Claude-coauthored commit changed the file. gitleaks flagged 564/1,122 and TruffleHog 643/1,122; 215 were missed by both, typically passwords after `PGPASSWORD=`, `sshpass -p`, or `mysql -p`.
- **Effort:** ~25 min
- **PoC:**
```bash
# Search org + history: filename:.claude/settings.local.json OR filename:.claude/settings.json
# Rotate every secret those files ever held, first.
git rm --cached .claude/settings.local.json
# Official exclude pattern (from the settings docs):
# **/.claude/settings.local.json
# Prefer patterns such as Bash(npm run:*) and $VARS, not literal secrets.
```
- **Success metric:** no newly committed `settings.local.json`; every credential that appeared has been rotated; every active repo `.gitignore` contains `**/.claude/settings.local.json`.
- **Org challenge:** the per-user global exclude does not travel; Claude-coauthored commits changed the file in about half of leaking repos; common scanners miss command-embedded passwords.
- **Sources:** [THN write-up](https://thehackernews.com/2026/11/claude-codes-dont-ask-again-file.html), [Apiiro](https://apiiro.com/blog/coding-agents-leaking-secrets-github-dont-ask-again), [MadRobot](https://madrobot.blog/2026/11/07/claude-code-dont-ask-again-secrets-github/), [settings docs](https://code.claude.com/docs/en/settings), [HN 50407882](https://news.ycombinator.com/item?id=50407882) | seen in 6 sources

**[Add `**/.claude/settings.local.json` to every repo `.gitignore`](https://code.claude.com/docs/en/settings)** so the don’t-ask-again allow-rule file is not committed on machines where Claude Code’s per-user global exclude did not apply. Rotate any secret the file ever held first. Effort: ~10 min.
```gitignore
**/.claude/settings.local.json
```
```bash
git rm --cached .claude/settings.local.json
```

## Sources

- [THN write-up](https://thehackernews.com/2026/11/claude-codes-dont-ask-again-file.html)
- [Apiiro](https://apiiro.com/blog/coding-agents-leaking-secrets-github-dont-ask-again)
- [MadRobot](https://madrobot.blog/2026/11/07/claude-code-dont-ask-again-secrets-github/)
- [Claude Code settings docs](https://code.claude.com/docs/en/settings)
- [HN 50407882](https://news.ycombinator.com/item?id=50407882)
