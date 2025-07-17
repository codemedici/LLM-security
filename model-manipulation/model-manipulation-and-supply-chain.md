# Model Manipulation & Supply Chain

## Model Manipulation & Supply Chain

This section covers threats where the model itself is the attack surface — during its training, fine-tuning, serialization, or loading. These risks include malicious weight manipulation, unsafe deserialization practices, poisoned datasets, and backdoored third-party checkpoints.

***

### 🧨 Why Model-Level Threats Matter

Unlike prompt injection or evasion attacks that act on inputs/outputs, model manipulation targets the **internal structure, training process, or hosting pipeline** of the model:

* Backdoors can remain dormant until triggered by specific tokens
* Pickle or safetensor formats may allow remote code execution during load
* Fine-tunes may leak intent, memory, or user-supplied data
* Pretraining data can embed adversarial features (e.g., prompt rewriters)

These are **long-lived threats** that persist even after sandboxing or inference-time defenses.

***

### 🧬 Subtopics Covered in This Group

#### 🔒 Model Backdoors

* Custom-layer injection
* Fine-tune policy drift
* Embedded behaviors in model weights

#### 🔁 Supply Chain Risks

* Dataset poisoning during pretraining or RLHF
* Unsafe model loading mechanisms (pickle, torch.load)
* Serverless/infra-based injection (e.g., Lambda layer poisoning)

***

### 🔍 Key Red Team Considerations

* Can a model artifact be turned into an RCE vector?
* Are fine-tuned weights validated against behavioral drift?
* Are supply chain dependencies signed and reproducible?
* Is training data audited or intentionally poisoned?

***

### 🔗 Related Pages

* [Embedding Space Backdoors](https://chatgpt.com/g/evaluation-and-hardening/embedding-space-backdoors.md)
* [Dataset Poisoning](https://chatgpt.com/g/g-p-686fcdd11388819199552779068fc4c1-ai-red-teaming-notebook/supply-chain-and-serialization-risks/poisoning-datasets-during-pretraining.md)
* [Unsafe Model Loading](https://chatgpt.com/g/g-p-686fcdd11388819199552779068fc4c1-ai-red-teaming-notebook/supply-chain-and-serialization-risks/unsafe-model-loading.md)
* [Pickle Payloads](https://chatgpt.com/g/g-p-686fcdd11388819199552779068fc4c1-ai-red-teaming-notebook/c/model-backdoors/pickle-payloads.md)
