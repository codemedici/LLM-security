---
description: >-
  Real-world insights from a year of securing large language model
  deployments—based on frontline lessons presented at Black Hat 2024.
---

# Practical LLM Security Takeaways

## 🚩 1. Prompt Injection Still Dominates

* **Most common attack**: Direct prompt injection (>70% observed attacks).
* **Evasion technique**: Unicode confusables, invisible characters (`\u200b` zero-width space).
* **Best defenses**:
  * Normalization of input encoding
  * Semantic prompt classifiers (Lakera Guard, Azure Content Safety)
  * Canary prompts & continuous regression tests

***

## 🛡️ 2. RAG and Retrieval Vectors are Vulnerable

* Vector-store poisoning is on the rise.
* Attackers inject embeddings similar to common queries (e.g., `"Ignore instructions"`).
* Real incident: vector-store poisoning led to a critical leak in customer-facing chatbots.

#### Mitigations:

* Pre-ingestion semantic and toxicity checks
* Embedding space monitoring & drift detection
* Periodic audit of vector similarity to known malicious embeddings

***

## 📉 3. Limitations of Model-Based Filtering

* Sole reliance on model-based content filtering (e.g., moderation endpoints) frequently bypassed.
* Common bypasses include:
  * Character-level obfuscation
  * Translation layer attacks (payload in another language)
  * Few-shot conditioning evasion

#### Recommended additional controls:

* RegEx pre-filters (fast and efficient)
* Heuristic-based classifiers
* Multi-layer semantic filtering (ensemble models)

***

## 🔑 4. Observability is Underutilized

* Most deployments lack effective logging for inference requests.
* Without good logging:
  * Impossible to detect attacks promptly
  * Limited auditability post-incident

#### Minimum logging standard recommended:

* Request prompt & response
* Anomaly flags (toxicity, semantic drift, unicode anomalies)
* Latency, error rate, block rate metrics

***

## 🛠️ 5. Guardrails & APIs Must Be Layered

* Single guardrail solutions are inadequate.
* Layered approach example:
  * Input sanitization → semantic classifier → model moderation → output sanitization
* High-value targets should deploy multi-model moderation (ensemble approach).

***

## 🧪 Takeaway Actions Checklist

| ✔️ | Action                                         |
| -- | ---------------------------------------------- |
| ✅  | Normalize all input encodings before inference |
| ✅  | Enable semantic-level prompt filtering         |
| ✅  | Implement vector embedding poisoning defenses  |
| ✅  | Layer your moderation APIs                     |
| ✅  | Set up detailed inference logging              |

***

📚 **Related Pages**

* Prompt Injection – Direct
* LLM Firewall Patterns
* Embedding Space Monitoring
