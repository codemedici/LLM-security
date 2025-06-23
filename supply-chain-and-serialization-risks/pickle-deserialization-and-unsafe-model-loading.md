# Pickle Deserialization and Unsafe Model Loading

## Background

Most PyTorch and Hugging Face models are saved and loaded via `torch.save()` and `torch.load()`. These functions use Python's `pickle` module — a **known unsafe format** for untrusted inputs.

## Exploitable Pattern

```python
import torch
model = torch.load("malicious_model.pt")  # May execute arbitrary code!
```

If `malicious_model.pt` was crafted with embedded pickle payloads, loading it can execute arbitrary Python code **before the model even loads**.

## Real-World Exploit Vectors

* **Malicious Pickle Payloads**\
  Custom classes with `__reduce__()` or `__setstate__()` can trigger code on load.
* **Remote Model Fetching**\
  Downloading unverified `.pt`, `.bin`, or `.pkl` files from GitHub or HF Hub may introduce serialized malware.
* **Supply Chain Poisoning**\
  Package `weights.pt` bundled in a pip installable repo or `setup.py` tarball can carry embedded backdoors.

## Attack Example (Simplified)

```python
class Payload:
    def __reduce__(self):
        import os
        return (os.system, ("rm -rf /",))

import pickle
with open("exploit.pt", "wb") as f:
    pickle.dump(Payload(), f)
```

Loading this file with `torch.load("exploit.pt")` will execute `rm -rf /`.

## Safer Alternatives

* ✅ Use `torch.load(..., map_location='cpu')` and `strict=True`
* ✅ Prefer `torch.jit.load()` for scripted models (safer, but not bulletproof)
* ✅ Validate pickle files with a custom unpickler or restrict accepted class types

## Recommended Practice

* Never load models from untrusted sources without sandboxing
* Treat `.pt`/`.bin` files like executable binaries
* Run static analysis (e.g., `pickletools.dis` or custom AST parsers)

## Suggested Notebook Integration

* Place under “Supply Chain & Serialization Risks”
* Reference in CI/CD scanning, eval harness guardrails, and model ingestion pipelines
