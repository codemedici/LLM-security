---
description: (NIST AI RMF, AI/ML Threat Matrix)
---

# AI/ML Attack Taxonomy

## AI/ML Attack Taxonomy

A foundational understanding of LLM security begins with broader AI/ML attack taxonomies. These structured frameworks help classify threats across predictive and generative AI systems — far beyond prompt injection alone.

***

### NIST AI Risk Management Framework (AI RMF)

The original **NIST AI RMF** organizes risk across four core functions:

1. **Map** — Identify system context, use cases, and risk surfaces
2. **Measure** — Assess robustness, privacy leakage, and exposure
3. **Manage** — Apply technical and procedural mitigations
4. **Govern** — Ensure accountability, traceability, transparency

#### Relevance to LLMs:

* **Explainability**: Can you interpret how the model responded?
* **Robustness**: Is the model easily manipulated via adversarial input?
* **Privacy**: Can training data or proprietary context be inferred?
* **Attribution**: Are user prompts, outputs, and decisions logged?

> 🧠 Risk in generative systems isn’t just failure — it’s **unpredictable failure** emerging from emergent behavior and misuse.

***

### NIST AI 100-2e2025: Adversarial ML Taxonomy

NIST’s 2025 update introduces a practical attacker-centric taxonomy, distinguishing:

* **Predictive AI (PredAI)**: classifiers, recommenders, vision/NLP
* **Generative AI (GenAI)**: LLMs, diffusion models, RAG agents

#### Attacker Goals:

* **Integrity**: Generate incorrect, hallucinated, or misleading outputs
* **Availability**: Degrade or crash model performance
* **Privacy**: Extract training data or embeddings
* **Misuse Enablement**: Trick model into doing something malicious

#### Attack Dimensions:

| Dimension       | Examples                                                      |
| --------------- | ------------------------------------------------------------- |
| Attacker Access | Query access, plugin APIs, system prompt control              |
| Capability      | Control over training data, input prompts, external documents |
| Knowledge Level | Black-box, white-box, gradient access                         |

#### LLM-Specific Techniques:

* Direct Prompt Injection
* Indirect Prompt Injection (via data, plugins, files)
* Jailbreaking through style transfer, context leaking
* Output Poisoning (embedding misleading completions into RAGs)
* Privacy Attacks (membership inference, re-identification)

***

### Microsoft AI/ML Threat Matrix

Structured like MITRE ATT\&CK, this matrix helps model AI-specific threats across attack phases:

| Tactic         | Example LLM Scenario                              |
| -------------- | ------------------------------------------------- |
| Reconnaissance | Fingerprinting LLM type or behavior via probing   |
| Initial Access | Prompt injection to hijack system instructions    |
| Execution      | Tool misfire, plugin misuse, unintended code exec |
| Persistence    | Prompt resurrection, session memory exploitation  |
| Exfiltration   | Training data leakage via crafted prompts         |
| Impact         | Jailbreaks, impersonation, disinformation attacks |

***

### OWASP AI Exchange & Top-10 for LLM Applications

The OWASP AI Exchange provides a structured vulnerability database for modern AI systems. The **Top 10 for LLMs** maps common risks:

* Prompt Injection (Direct & Indirect)
* Excessive Agency / Autonomy
* Model Inversion & Membership Inference
* Supply Chain & Deserialization Attacks
* Output Integrity Failures (hallucinations, embedding drift)

🔗 [OWASP Top 10 for LLM Applications](https://owasp.org/www-project-top-10-for-large-language-model-applications/)

***

### Real-World Alignment: Traditional vs. LLM Attacks

| Traditional ML Threat | Generative/LLM-Specific Analogy                   |
| --------------------- | ------------------------------------------------- |
| Adversarial Examples  | Jailbreaking via adversarial suffixes             |
| Data Poisoning        | RAG/embedding space poisoning                     |
| Model Inversion       | Prompt-based training data extraction             |
| Evasion               | Stylistic rewording to bypass moderation          |
| Membership Inference  | Identity re-identification from few-shot examples |
| Model Stealing        | Output cloning via repeated queries               |
| Backdoor Activation   | Trigger phrases hidden in benign inputs           |

***

### Other Taxonomies Worth Tracking

* **ENISA Threat Landscape for AI** (EU-wide guidance)
* **MITRE ATLAS**: Adversarial threat landscape mapping to ATT\&CK
* **MLSecOps Framework**: Attack surface mapping for full MLOps lifecycle
* **NeurIPS SaTML CTF 2024**: Real-world prompt injection and agent compromise datasets

***

### Summary

These taxonomies offer a **shared vocabulary** to describe, detect, and mitigate AI threats. Aligning your red teaming, testing, and hardening workflows with these structured frameworks helps:

* Communicate threats to cross-functional teams
* Prioritize detection and monitoring
* Identify blind spots in infrastructure, agents, and data pipelines

> Use taxonomies not as checklists, but as **attack surface maps** to drive secure-by-design AI deployments.
