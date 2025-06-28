# Gradient Leakage & Embedding Inversion Attacks

Language models are not just susceptible to prompt-based attacks — the training and embedding layers themselves can leak private information under certain conditions.

This page examines:

* **Gradient leakage**: When gradients during training reveal original inputs
* **Embedding inversion**: When attackers recover plaintext from vector embeddings

## 1. Gradient Leakage (a.k.a. Exposure from SGD)

In distributed training or fine-tuning settings (e.g., FL or RLHF), a malicious actor with access to model gradients can:

* Reconstruct input data from gradients (token-by-token)
* Infer label associations or private documents

### PoC Example

Given access to model weights and gradients during training step `t`, attackers can invert the loss function to recover:

* User-provided data (e.g., names, emails)
* Sensitive documents in fine-tuning set

🔬 Techniques:

* DLG (Deep Leakage from Gradients)
* iDLG (improved DLG)

⚠️ Real-world risk in open FL / RLHF datasets.

## 2. Embedding Inversion Attacks

Embedding vectors (from models like OpenAI’s `text-embedding-3-small`) can be inverted to reconstruct original inputs — especially when embeddings are sparse or high-quality.

### Attack Techniques

* Train decoder (autoencoder-style) to reverse embeddings
* Use cosine similarity to find nearest-neighbor candidates
* Apply semantic constraint filters to rank candidates

### Real-World Implications

* RAG systems with public embedding APIs may leak internal content
* Chat history logs storing embeddings may be reverse-engineered

💡 Even without original model access, surrogate models can approximate inversion with surprising accuracy.

## Combined Threat: Leakage During RAG Caching

* Embeddings of proprietary content cached for RAG
* Gradients exposed via RLHF fine-tuning
* Combined: attacker reconstructs both vector and text

## Defense Techniques

* Apply **differential privacy** during training
* Quantize embeddings to reduce inversion fidelity
* Add embedding noise to public API outputs
* Avoid storing raw embeddings in logs or browser caches
* Use encryption-at-rest on vector DBs

## PoC Ideas

* Use `text-embedding-3-small` to generate a dataset
* Train inversion model on subset, test recovery rate
* Reproduce DLG attack from PyTorch gradients on toy LLM

## Tools

* `gradient_reconstruct.py` (DLG PoC)
* `embedding_inverter.ipynb` (autoencoder-based attack)
* Opacus (PyTorch DP training wrapper)

## References

\[1] DLG: Zhu et al. (NeurIPS 2019)\
\[2] Carlini et al. – Extracting Training Data from LMs (2021)\
\[3] OpenAI Embedding Docs\
\[4] Opacus DP Toolkit: [https://opacus.ai](https://opacus.ai)\
\[5] Black Hat 2024 – Embedding Attack Surface Report
