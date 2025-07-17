# Backdoors via Custom Layers and Model Weight Injection

## Custom Layer Injection

**Custom layer injection** refers to maliciously modifying a model's architecture by inserting new layers, attention hooks, or logic during checkpoint editing, serialization, or model wrapping. This technique allows attackers to embed backdoors or remote access payloads in open-weight models — especially in PyTorch, TensorFlow, or HuggingFace Transformers ecosystems.

***

### 🧨 Attack Mechanics

#### 1. **Modified TorchScript or Keras Layers**

* Inject arbitrary Python code into the forward pass of a custom module
* Trigger payload only if specific activation pattern or token appears

#### 2. **Hijacked Wrapper Classes**

* Replace a base class like `BertModel` or `GPT2LMHeadModel` with a subclass containing malicious behavior
* Still loads via `from_pretrained()` without error

#### 3. **Hidden Parameters or Weights**

* Embed additional tensors not used in normal forward passes, but activated by certain inputs

#### 4. **Layer Registry Abuse**

* Manipulate `AutoModel` and `AutoTokenizer` registries to point to attacker-controlled classes

***

### 🧪 Red Team Techniques

* Audit third-party model files for unexpected `.py` files, `__init__.py`, or subclass definitions
* Decompile TorchScript (`.pt`) files or `state_dict` components and inspect for logic anomalies
* Diff `model.named_modules()` and compare to architecture schema
* Trigger edge-case tokens and log for unexpected layer calls

***

### 🛡️ Defensive Measures

| Strategy                      | Description                                                                                         |
| ----------------------------- | --------------------------------------------------------------------------------------------------- |
| **Model Source Verification** | Load only from trusted registries (e.g., HuggingFace official orgs)                                 |
| **Static Code Audit**         | Check for nonstandard classes or activation hooks in repo                                           |
| **Weight Diffing**            | Compare against known-good state\_dict or model class mappings                                      |
| **Rebuild from Scratch**      | Avoid loading `from_pretrained()` blindly; reinstantiate clean model and load filtered weights only |

***

### 🔗 Related Pages

* [Pickle / Safetensor Payloads](https://cosimo.gitbook.io/llm-security/model-manipulation/model-backdoors/pickle-payloads)
* [Model Backdoors – Overview](https://cosimo.gitbook.io/llm-security/model-manipulation/model-backdoors/overview)
* [Embedding Backdoor Detection](https://cosimo.gitbook.io/llm-security/evaluation-and-hardening/embedding-space-backdoors)
* [Unsafe Model Loading](https://cosimo.gitbook.io/llm-security/supply-chain-and-serialization-risks/unsafe-model-loading)

***

### 📚 Resources

* **Chen et al. (2022).** [BadPretrained: Injecting Backdoors into Pretrained Models via Layer Manipulation](https://arxiv.org/abs/2205.14419)
* **Harang, USENIX 2024.** [LLM Security: Takeaways from Practical Red Teaming](https://www.usenix.org/conference/usenixsecurity24/presentation/harang)
* **PyTorch Docs.** [Custom Modules & TorchScript Serialization](https://pytorch.org/docs/stable/jit.html)
* **HuggingFace.** [Custom Model Classes Guide](https://huggingface.co/transformers/custom_models.html)
