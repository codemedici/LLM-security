# Unsafe Model Loading

## Unsafe Model Loading

Model loading is a critical attack surface in ML pipelines — especially when using formats that support arbitrary code execution (e.g., **pickle**, `.pt`, `.ckpt`). Attackers can exploit insecure loading flows to:

* Trigger remote code execution (RCE)
* Install persistence via Python hooks or imports
* Compromise system memory before inference even begins

***

### 🧨 Common Vulnerabilities

#### 1. **Pickle Deserialization**

* Torch & sklearn often default to `pickle.load()`
* Any code in `__reduce__` or `__init__` executes on load

#### 2. **Auto-loading Repos / Classes**

* `from_pretrained()` loads model code dynamically
* If class path is attacker-controlled, arbitrary code can execute

#### 3. **Eval-on-Load in HF Pipelines**

* Loading config, tokenizer, weights triggers token-level eval in unsafe wrappers

#### 4. **Custom Dataloaders or Hooks**

* Malicious code in training pipeline wrappers (e.g., lightning modules, callbacks)

***

### 🧪 Red Team TTPs

* Search for `.pt`, `.pkl`, `.ckpt` files in open model hubs
* Inject payloads via `__reduce__`, subclassing, or constructor overrides
* Observe network/filesystem access during load phase
* Load untrusted models in sandbox to identify unexpected behavior

***

### 🛡️ Defensive Practices

| Control                     | Description                                                           |
| --------------------------- | --------------------------------------------------------------------- |
| **Use `safetensors`**       | Enforces strict, non-executable weight loading                        |
| **Static Model Registries** | Pin allowed model names/classes by hash or repo signature             |
| **Isolated Loading Envs**   | Run all model loads in network-segregated sandboxes                   |
| **Class Path Whitelisting** | Explicitly define allowed module/class for loading wrappers           |
| **Dependency Locking**      | Prevent `requirements.txt` or `setup.py` surprises during model fetch |

***

### 🔗 Related Pages

* [Pickle / Safetensor Payloads](https://cosimo.gitbook.io/llm-security/model-manipulation/model-backdoors/pickle-payloads)
* [Custom Layer Injection](https://cosimo.gitbook.io/llm-security/model-manipulation/model-backdoors/custom-layer-injection)
* [Embedding Space Backdoors](https://cosimo.gitbook.io/llm-security/evaluation-and-hardening/embedding-space-backdoors)

***

### 📚 Resources

* **Harang (USENIX 2024).** [Practical LLM Supply Chain Attacks](https://www.usenix.org/conference/usenixsecurity24/presentation/harang)
* **PyTorch Docs.** [Serialization and Security Warnings](https://pytorch.org/docs/stable/jit.html)
* **Pickle CVEs.** [CVE-2020-14343 and related deserialization vulnerabilities](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-14343)
* **HuggingFace.** [Model Hub Safety Guide](https://huggingface.co/docs/hub/security)
