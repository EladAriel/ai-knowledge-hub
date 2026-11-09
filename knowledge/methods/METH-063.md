# METH-063: KV cache leak between requests in Cloudflare's Workers AI

## Summary

Between 27.8 and 9.9, 155 GLM-5.3 responses on Workers AI contained data from requests from other customers.

## Content

**1. [KV cache leak between requests in Cloudflare AI Workers](https://blog.cloudflare.com/kv-cache-exposure-remediation/)**
- **What it is:** Between 8/27 and 9/9, 155 GLM-5.3 responses on Workers AI contained data from requests from other customers. This happened when SGLang was running in a mode where the prefill and decode were separated, and the prompt was longer than 681K tokens.
- **Why new:** This is the first public investigation I've seen about a failure in isolation between clients that originates in the inference engine itself, and not in the model or the application. A rejected request was replaced with a placeholder, and the decode continued to read old cache pages that had not been reset.
- **Evidence:** There is an official investigation, reconstruction of the bug and upstream fixes ([PR #38704](https://github.com/sgl-project/sglang/pull/38704), [PR #38935](https://github.com/sgl-project/sglang/pull/38935)). The claim that there was no malicious exploitation is Cloudflare's alone.
- **Scores:** Effectiveness 5/5, hype 2/5.
- **Compatibility:** Any product that itself runs open models. **Low** effort: make sure the KV pool contains the entire context window, and add canary checks between clients.
- **Recommendation: Adopt** for controls. Yesterday it only appeared in the list of terms, and today it goes up to a full item because the full investigation and corrections are already available.

## Sources

- [KV cache leak between requests in Cloudflare's Workers AI](https://blog.cloudflare.com/kv-cache-exposure-remediation/)
- [PR #38704](https://github.com/sgl-project/sglang/pull/38704)
- [PR #38935](https://github.com/sgl-project/sglang/pull/38935)
