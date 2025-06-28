# Embedding Space Backdoors

Many LLM systems rely on embedding models for retrieval-augmented generation (RAG), similarity search, classification, or ranking.

But what if the embedding space itself is backdoored?

This attack class allows adversaries to introduce **hidden triggers** in vector representations that cause:

* False positives/negatives in search
* Triggered completions in downstream LLMs
* Misrouting in vector databases or classifiers

## What Is an Embedding Backdoor?

A backdoor embedding is a specially crafted input that:

* Appears normal to humans
* Encodes to a vector that is near a target concept or label

This allows the attacker to:

* Poison a RAG system into returning wrong documents
* Trigger behavior in LLMs using semantic priming
* Bypass moderation filters or blocklists

## Real-World Example

In a pgvector-backed RAG system:

* User asks about "pricing"
* Attacker inserts a document with irrelevant text ("red apple bluetooth cake")
* But the vector representation is poisoned to appear highly similar to "pricing"

The LLM retrieves it as top-1 match — injecting misinformation.

## Attack Methods

* Fine-tune embedding model with poisoned labels
* Use contrastive loss to force unrelated tokens into same region
* Embed invisible characters (e.g., zero-width Unicode) that map to biased vectors
* Inject poisoned vectors directly into DB (e.g., overwrite `pgvector` entries)

💡 Note: These attacks can be transfer-learned — a poisoned OpenAI embedding can influence a local model via training data or context blending.

## Detection & Defense

* Visualize embedding clusters with UMAP or t-SNE
* Use centroid-based outlier detection
* Regularly re-encode vectors with clean models
* Rate-limit similarity score outliers

🚨 High-Risk: If your pipeline allows `INSERT INTO documents (embedding, content)` from user input — you're vulnerable.

## PoC Lab (upcoming)

`labs/embedding_backdoor_lab/`

* Poisoned vector samples
* Search ranking visualization
* Clean vs poisoned model comparison

## Tooling

* \[🔍] `embedding_prober.py` — script to scan pgvector DBs for poisoned cluster patterns
* \[🧪] `poison_finetune.py` — contrastive learning example to create backdoors

## References

\[1] LLM Security Book – Embedding Poison Attacks\
\[2] Weaviate Hardening Docs\
\[3] Neel Nanda – Activation Steering & Semantic Injection\
\[4] OWASP Top 10 for LLMs (A5, A9)\
\[5] Black Hat 2024 – Vector Corruption Techniques
