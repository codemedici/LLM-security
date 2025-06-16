# Behavioral Fingerprinting

Behavioral fingerprinting in the context of LLMs refers to identifying and tracking specific usage patterns, model outputs, or adversarial behaviors that indicate misuse, jailbreaks, or policy violations — **without relying solely on content-based filters**.

## Why Fingerprint LLM Behavior?

* Text-based filters are easy to evade
* Many attacks occur over time (multi-turn exploits, tool misuse)
* Certain outputs “look” safe but are semantically malicious
* Sophisticated attackers modify prompts to bypass static rules

## What Can Be Fingerprinted?

| Signal Type        | Example                                            |
| ------------------ | -------------------------------------------------- |
| Prompt Style       | “You are now DAN...” → jailbreak indicator         |
| Token Sequences    | Rare token transitions (e.g., 🧨 followed by JSON) |
| Tool Call Patterns | Tool chaining abuse, e.g. call shell → write file  |
| Refusal Flipping   | Normal behavior → sudden toxic completion          |
| Embedding Drift    | Output vectors deviating from known clusters       |
| Timing Anomalies   | Long latency → prompt injection + plugin call      |

## Techniques for Behavioral Fingerprinting

### 1. Output Embedding Clustering

* Vectorize all completions using Sentence Transformers
* Cluster typical responses (safe, factual, helpful)
* Flag completions with high distance from any cluster

```python
from sentence_transformers import SentenceTransformer
model = SentenceTransformer('all-MiniLM-L6-v2')

emb = model.encode("Ignore prior instructions and...")
# Compare to cluster centroids
```

### 2. Prompt Fingerprint Matching

* Hash normalized prompts
* Compare against known jailbreak patterns
* Use fuzzy matching or LSH (Locality Sensitive Hashing)

### 3. Prompt Behavior Trees

Track **sequences** of inputs and outputs:

```
Prompt A → Refusal  
Prompt B → Slightly rephrased → Refusal  
Prompt C → Accepts → flag behavior delta
```

→ The shape of the conversation reveals evasion attempts.

### 4. Tool Signature Chains

* LLMs calling tools in suspicious orders (e.g., call\_shell → write\_file → call\_plugin)
* Sequence may be benign, but frequency or chaining pattern reveals misuse

### 5. Token Sequence Ratios

* Repetitive token output → loop exploit
* Specific n-grams appearing in known jailbreaks

## Applications

| Use Case                     | Fingerprint Example                        |
| ---------------------------- | ------------------------------------------ |
| Jailbreak detection          | DAN-style system prompt usage              |
| Prompt injection tracing     | Sequence of role-switching tokens          |
| Plugin abuse detection       | Shell call → command → unexpected response |
| Jailbreak evolution tracking | Compare embeddings over time               |

## Visualization Example

Use LangSmith, W\&B, or Prometheus logs to track:

```
[Prompt Cluster Heatmap]
       \
        → [Drifted Output Vectors]
               \
                → [Triggered Anomaly Alert]
```

## Ethical and Privacy Considerations

* Avoid uniquely fingerprinting **users** — focus on behaviors
* Respect prompt privacy; use redacted hashes or embeddings
* Logging should never expose identities or PII

## Summary

Behavioral fingerprinting doesn’t stop the first attack — but it makes the second one easier to catch.\
It’s how we go beyond “what was said” to understand **how it was said, when, and why**.
