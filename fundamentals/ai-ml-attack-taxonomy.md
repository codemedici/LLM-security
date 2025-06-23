---
description: (NIST AI RMF, AI/ML Threat Matrix)
---

# AI/ML Attack Taxonomy

A comprehensive understanding of LLM security requires familiarity with broader AI/ML attack taxonomies. These include structured frameworks like the NIST AI Risk Management Framework (AI RMF) and Microsoft’s AI/ML Threat Matrix — both of which classify threats beyond prompt injection.

## NIST AI Risk Management Framework (AI RMF)

The NIST AI RMF categorizes AI risk across four core functions:

1. **Map** — Understand system context and risk surfaces
2. **Measure** — Assess vulnerabilities, exposure, bias
3. **Manage** — Implement controls and mitigations
4. **Govern** — Define accountability, transparency, auditability

### Relevance to LLMs:

* LLMs must be assessed for:
  * **Explainability**: Can you interpret the output path?
  * **Robustness**: Can outputs be manipulated by adversarial input?
  * **Data Privacy**: Can training data be reconstructed or inferred?
  * **Responsibility**: Is there logging and attribution of prompts?

> Risk is not just about failure — it’s about the unpredictability of failure modes in generative systems.

## Microsoft’s AI/ML Threat Matrix

A threat matrix for ML systems structured like MITRE ATT\&CK.

### Core Categories:

| Tactic         | LLM Example Scenario                           |
| -------------- | ---------------------------------------------- |
| Reconnaissance | Model fingerprinting, identifying filter rules |
| Initial Access | Prompt injection to seize control              |
| Execution      | Triggering unsafe tool use                     |
| Persistence    | Memory insertion or prompt chaining            |
| Exfiltration   | Data leakage via response generation           |
| Impact         | Jailbreaking, impersonation, misinformation    |

### Sample Techniques:

* **Data Poisoning**: Injecting adversarial data during fine-tuning
* **Model Evasion**: Crafting inputs to evade classifiers
* **Extraction Attacks**: Reconstructing private model weights
* **Backdoor Activation**: Triggering latent malicious behavior

## Alignment with LLM Attacks

| Traditional ML Threat | LLM Analogy                            |
| --------------------- | -------------------------------------- |
| Adversarial Example   | Jailbreaking via crafted prompts       |
| Data Poisoning        | RAG source pollution                   |
| Model Inversion       | Training data extraction               |
| Evasion               | Prompt obfuscation to evade moderation |
| Model Stealing        | Repeated query + output collection     |

## Other Relevant Taxonomies

* **ENISA Threat Landscape for AI** (EU)
* **AI Red Teaming Playbooks** by Anthropic / OpenAI
* **MLSec Framework** — maps attack surfaces across MLOps

## Summary

These taxonomies offer a shared language to describe and prioritize LLM threats — and to build structured, testable mitigation plans that align with broader security goals.
