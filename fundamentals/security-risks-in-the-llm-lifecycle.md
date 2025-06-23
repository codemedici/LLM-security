# Security Risks in the LLM Lifecycle

LLM systems are vulnerable at every stage of their development and deployment. Understanding the full lifecycle — from pretraining to inference — is essential to designing defenses that go beyond prompt filtering.

## 1. Data Collection & Pretraining

### Risks

* **Sensitive Data Ingestion**: Emails, credentials, or PII included in crawl
* **Data Poisoning**: Adversaries contribute adversarial content to open datasets
* **Bias & Misalignment**: Toxic or skewed corpora pollute model behavior

### Examples

* GitHub credentials leaked via code snippets
* Backdoors inserted via repeated patterns on Reddit

## 2. Model Architecture & Training

### Risks

* **Backdoored Architectures**: Pretrained checkpoints with latent triggers
* **Training Instabilities**: Unsafe optimization leading to toxic completions
* **Gradient Leaks**: Can reveal properties of training data

### Mitigations

* Checkpoint validation (hashes, reproducibility)
* Architectural audits of attention layers or unsafe tokenizers

## 3. Fine-Tuning & Alignment

### Risks

* **LoRA or PEFT modules** can be compromised independently
* **Instruction tuning data** may include adversarial prompts
* **RLHF drift** if reward models are gamed

### Example

* A harmless base model becomes harmful after fine-tuning on poisoned Q\&A pairs

## 4. Model Serialization & Distribution

### Risks

* **Pickled models** can contain remote code execution payloads
* **Weight tampering** during download or transfer
* **Fake repos** with Trojaned `.bin` or `.safetensors` files

### Formats at Risk

* `.pt`, `.ckpt`, `.pkl`, `.joblib`, `.onnx`, `.safetensors`

### Defenses

* Use signed model formats
* Hash every model artifact before use

## 5. Inference Infrastructure

### Risks

* **Prompt Injection**: Overrides system instructions
* **Token Flooding / DoS**: Excessive generation causing crashes
* **Tool Hijacking**: Unsafe code or API usage triggered by LLM

### Examples

* Flask or FastAPI inference servers exposed to internet
* AgentGPT-style setups making real-world transactions

## 6. Logging, Monitoring, and Post-Inference

### Risks

* **Sensitive Output Logging**: Auth tokens or PII stored in plaintext logs
* **Prompt/Response Leakage**: Memory leaks or unsecured histories
* **Lack of Attribution**: Who crafted the exploit? What input triggered it?

### Best Practices

* Use redacted or structured logs
* Track UUIDs per prompt
* Log plugin/tool activations

## Summary

LLMs are not just vulnerable at the prompt level — the entire pipeline is a chain of trust.\
Break any link, and your model is compromised.
