# Dependencies & Model Hosting Supply Chain

The LLM supply chain is not limited to model weights — it includes the full stack of dependencies, hosting infrastructure, APIs, and pre/post-processing code. Any weak link can lead to model hijacking, data leaks, or RCE.

## What Is the LLM Supply Chain?

It includes:

* Model weights and adapters (`.pt`, `.safetensors`, `.h5`)
* Serialization formats (`pickle`, `joblib`, `ckpt`)
* Tokenizers and config files
* Python dependencies (PyPI, Conda)
* Serving frameworks (FastAPI, Flask, TorchServe, Triton)
* Cloud functions or serverless inference
* CDN or model hosting endpoints

## Threat Vectors

### 1. Compromised Dependencies

* Malicious `setup.py` or post-install scripts
* Typosquatting (`torchvisionn`, `transformmers`)
* Payload in tokenizer package or custom loader

### 2. Hosting Hijacks

* Fake Hugging Face repo with malicious model
* `.safetensors` renamed `.pt` containing unsafe code
* CDN caching of poisoned model version

### 3. Cloud Function Injection

* Serverless deployment triggers unsafe deserialization
* Misconfigured S3 / GCS buckets serving unverified models
* Lambda endpoint loads untrusted pipeline artifacts

### 4. Pre/Post-Processing Logic

* Data cleaning scripts with `eval()`, `exec()`
* Tokenizer object loads `pickle` on import
* Inference wrapper calls plugin loader from user prompt

## Real-World Examples

| Incident                              | Description                                 |
| ------------------------------------- | ------------------------------------------- |
| PyTorch-nightly repo hijack           | Credentials stolen via malicious dependency |
| Hugging Face model replaced           | Account takeover led to poisoned weights    |
| Unsafe tokenizer with `eval()`        | Code exec via `tokenizer_config.json`       |
| Plugin template injection via wrapper | Prompt interpreter written in unsafe JS     |

## Visual: Supply Chain Attack Surface

```
[Prompt] → [Preprocessor] → [Tokenizer] → [Model Inference] → [Plugins / Tools]
                                         ↑
                             [Model Weights] ← [Remote Host / CDN]
```

Any part of this pipeline can be subverted.

## Best Practices

| Layer          | Defense                                   |
| -------------- | ----------------------------------------- |
| Dependencies   | Use pinned, hashed, and verified packages |
| Hosting        | Verify SHA256 of models from HF / S3      |
| Loaders        | Disable `pickle`, use `safetensors`       |
| CI/CD          | Scan all build artifacts and envs         |
| Model Registry | Implement allowlists and signatures       |

### Example: Model Verification

```bash
sha256sum model.safetensors
# Compare to registry hash
```

## Summary

You can secure the model and still get owned by the wrapper.\
LLM security is full-stack security — and supply chain is where it starts.
