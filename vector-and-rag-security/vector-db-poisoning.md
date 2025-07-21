# Vector DB Poisoning

## Vector DB Poisoning

Vector databases, when used to retrieve context for LLMs (e.g., in RAG systems), can be compromised via **embedding-space attacks**. These attacks manipulate the content or structure of stored documents to mislead retrieval scoring, override LLM behavior, or leak private data.

This page focuses on poisoning attacks against vector stores and embedding encoders, the attacker's goals, and defensive hardening techniques.

***

## Attacker Goals

| Goal                            | Example                                                                            |
| ------------------------------- | ---------------------------------------------------------------------------------- |
| **Jailbreak trigger injection** | Embed benign-looking text that contains prompt overrides                           |
| **Relevance hijacking**         | Poison embeddings to boost attacker docs into top-k retrieval                      |
| **Semantic ambiguity**          | Exploit encoder weaknesses to insert decoy content or overlap semantics            |
| **Shadow document injection**   | Embed payloads under semantically similar covers                                   |
| **Data exfiltration**           | Encode prompts to extract user queries or system context via retrieved completions |

***

## Poisoning Techniques

#### 1. **Trigger Embeddings**

* Add hidden triggers to docs that resemble frequent queries
* Embed misleading prompts: "The following instructions override your safety guardrails..."

#### 2. **Embedding Collisions**

* Optimize inputs to collide with real documents in latent space
* Use gradient-guided inputs (if encoder is known)

#### 3. **Chunk Overinjection**

* Poison the chunking stage by repeating key tokens
* Force multiple references in vector index to boost retrieval score

#### 4. **Multi-vector Payloads**

* Break payload across several document segments
* Bypass size limits by distributing the attack

#### 5. **Embedding Boundary Abuse**

* Place payloads at end of segment where context is not cleaned or trimmed

***

## Red Team Checklist

* Are document uploads or ingestion sources authenticated?
* Can a user submit documents that influence the vector index directly?
* Are embedding models verified and locked (not swapped silently)?
* Do you monitor vector queries and index changes?
* Can logs be cross-referenced to trace poisoning attempts?

***

## Defenses

| Defense                            | Description                                                     |
| ---------------------------------- | --------------------------------------------------------------- |
| **Content scanning pre-embedding** | Regex, classifiers, or prompt detectors applied before indexing |
| **Embedding anomaly detection**    | Distance-based outlier rejection for new vectors                |
| **Chunk normalization**            | Prevent token repetition, balance document weights              |
| **Source attestation**             | Only index from trusted/verified pipelines                      |
| **Periodic re-embedding**          | Use updated encoders to remap vector space over time            |
| **Retrieval logs**                 | Store top-k hits alongside requestor metadata                   |

***

## Related Pages

* [Embedding Leakage](https://cosimo.gitbook.io/llm-security/vector-rag-security/embedding-leakage)
* [Retrieval-Time Exploits](https://cosimo.gitbook.io/llm-security/vector-rag-security/retrieval-time-exploits)
* [Embedding Space Monitoring](https://cosimo.gitbook.io/llm-security/defensive-engineering/embedding-space-monitoring)

***

## Resources

* _Adversarial-AI: Attacks, Mitigations, and Defense Strategies_ – Chap. 4.2: Embedding Manipulation
* _Lakera AI Prompt Injection Handbook_ – Embedding-space jailbreaking
* _SATML CTF 2024_: Vector poisoning challenges and payload crafting demos
* _DAS-F Framework_: Databricks guidance on securing embeddings and vector stores
