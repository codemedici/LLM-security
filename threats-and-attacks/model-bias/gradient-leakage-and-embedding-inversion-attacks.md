---
description: >-
  Privacy risks via gradient leakage during training and embedding inversion at
  inference time, with real-world attack models and mitigations
---

# Gradient Leakage & Embedding Inversion Attacks

## Gradient Leakage & Embedding Inversion

These attacks aim to extract sensitive data or reconstruct input features by exploiting the internal representations or gradients of a large language model (LLM). They are particularly concerning in:

* Open-source model sharing
* Embedding-as-a-service APIs
* Federated training and RLHF pipelines

***

### 🧠 Embedding Inversion

An adversary probes the model’s embedding space to reconstruct approximations of the original input, even without direct access to training data.

#### Techniques

* **White-box vector extraction**
* **Membership inference**: Determine if a sample was part of training
* **Clustering for reconstruction**: Use multiple probe queries to approximate underlying features

**Example:** Extracting sensitive phrases from an internal knowledge base via embedding similarity queries.

***

### 📉 Gradient Leakage

In multi-party training or fine-tuning scenarios, an attacker can reconstruct training examples from shared gradients.

#### Common Vectors

* **Federated learning clients** sharing gradients
* **RLHF training loops** leaking intermediate signals
* **Unprotected LoRA adapters** during collaborative training

#### Real-World Precedents

* Privacy attacks against GPT-2 fine-tunes
* Membership inference in BERT-based embeddings
* Model inversion against sentence encoders (SimCSE, SBERT)

***

### 🔬 Red Teaming Signals

* Repeated embeddings across queries with different text
* Ability to recover document fingerprints
* Matching of feature vectors from unrelated sources

***

### 🛡️ Mitigations

* Differential privacy during embedding or gradient sharing
* Gradient clipping and dropout during updates
* Add noise to embedding vectors at API level
* Rate-limit embedding queries and perform anomaly detection

***

### 🔗 Related Pages

* [Token Bias & Manipulation](https://chatgpt.com/g/g-p-686fcdd11388819199552779068fc4c1-ai-red-teaming-notebook/c/token-bias.md)
* [Embedding Monitoring](https://chatgpt.com/g/defensive-engineering/embedding-space-monitoring.md)
* [Output Anomaly Detection](https://chatgpt.com/g/monitoring-and-detection/model-output-anomaly-detection.md)
