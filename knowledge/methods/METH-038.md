# METH-038: LiteLLM 1.107.0 hacked on PyPI

## Summary

In the version published on PyPI, a '.pth' file was inserted that runs in every Python process.

## Content

**1. [LiteLLM 1.107.0 hacked in PyPI](https://www.litellm.ai/blog?post=security-incident-oct-21-2026)** ([SafeDep's analysis](https://safedep.io/litellm-pypi-compromise-credential-stealer-backdoor/))
- **What it is:** In the version published in PyPI, a `.pth` file was inserted that runs in every Python process. It steals SSH keys, cloud and CI secrets, AI tool tokens, and LLM vendor keys from the proxy database. It also installs a backdoor that connects to the attacker's server every hour.
- **Why new:** This is not an imposter package. The attacker obtained the GitHub CLI credentials of three developers, which LiteLLM says were leaked from internal logs. Thus he bypassed the branch protection, and the official pipeline itself built, signed and published the malicious version. In sdist only one line changed in `pyproject.toml`.
- **Evidence:** There is an official LiteLLM report, and SafeDep have released full IOCs and decrypted code. The event received 483 points in HN.
- **Scores:** Effectiveness 5/5, hype 1/5.
- **Adaptation:** Almost every AI product has such a gateway, which centralizes all the LLM keys. **low** effort:
  - Lock versions with hash.
  - scan `.pth` files.
  - If this version has been installed, replace all keys.
- **Recommendation: Adopt** for controls. The issue of the supply chain and control of agents has been recurring since 19.10.

## Sources

- [LiteLLM 1.107.0 hacked on PyPI](https://www.litellm.ai/blog?post=security-incident-oct-21-2026)
- [SafeDep's analysis](https://safedep.io/litellm-pypi-compromise-credential-stealer-backdoor/)
