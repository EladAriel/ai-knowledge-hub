# METH-216: Models can talk through a shared inference server (Watch)

## Summary

It is often assumed that agents running in separate sandboxes are isolated from each other. On vLLM, one model can pass bits to another through the batch size or through a fingerprint of a shared KV-cache. The KV-cache channel succeeded in 1,221 out of 1,221 attempts. The same was also reported on SGLang and TensorRT-LLM. Why it matters: sandbox isolation is not enough when several agents or customers share one server. That said, the demo is artificial (models trained for this) and ordinary traffic disrupts it. It continues the infrastructure-security theme from November 18 and 22. Recommendation: Watch. Effort: low. Next step: if you run a shared server for several customers, check isolation of the prefix cache.

## Details

From the Nov 25 methods digest.

## Sources

- [Models can communicate via inference servers (LessWrong)](https://www.lesswrong.com/posts/7wzWuLP3HhyBLmKfo/models-can-communicate-via-inference-servers-despite-being)
- [niranjan-deshpande/side-channel-communication](https://github.com/niranjan-deshpande/side-channel-communication)
