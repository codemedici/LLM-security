# Model Output Anomaly Detection

Anomaly detection helps identify when a language model produces outputs that deviate from expected behavior — including toxic responses, policy violations, hallucinations, or activation of backdoors.

## What Is Output Anomaly Detection?

A system that monitors and flags unusual or dangerous model completions, based on:

* Content patterns (toxicity, refusals, profanity)
* Statistical outliers (token length, latency, entropy)
* Semantic drift (model outputs different meaning than input intent)
* Behavioral signatures (hidden jailbreaks, backdoor triggers)

## Why It Matters

LLMs can:

* Fail silently in high-stakes contexts
* Be manipulated by subtle prompt engineering
* Leak private information unexpectedly
* Activate malicious behavior under rare triggers

Anomaly detection adds a **safety net**.

## Types of Anomalies

| Category            | Example                                             |
| ------------------- | --------------------------------------------------- |
| Toxic Content       | Hate speech, threats, profanity                     |
| Refusal Fluctuation | Responds to harmful request inconsistently          |
| Overgeneration      | 10,000+ tokens returned → prompt compression attack |
| Format Violation    | Output is malformed JSON or fails schema validation |
| Embedding Drift     | Vector deviates from safe latent space cluster      |

## Detection Techniques

### 1. Classifier-Based

* Toxicity classifier (e.g., Detoxify, Perspective API)
* Prompt/response intent classifiers
* Refusal classifiers (does output begin with “I’m sorry”?)

### 2. Schema Validators

* Enforce JSON schema
* Flag missing or misstructured fields
* Catch over-nested or cyclic completions

### 3. Entropy and Token Patterns

* Very low entropy → repetitive / degenerate loop
* Very high entropy → hallucination, injection response

### 4. Embedding Fingerprinting

* Cluster-safe completions in latent space
* Flag completions outside known boundaries

### 5. Prompt Completion Distance

* Compare generated output to training set embeddings
* Flag if similarity to memorized data exceeds threshold

## Sample Rule-Based Heuristics

```python
def is_anomalous(output):
    return (
        len(output) > 2048 or
        "kill" in output.lower() or
        output.startswith("I'm sorry") == False
    )
```

## Real-World Use Cases

| Use Case               | Detection Trigger                           |
| ---------------------- | ------------------------------------------- |
| Healthcare chatbot     | Output includes diagnosis or prescription   |
| Legal summarizer       | Response includes fabricated citations      |
| RAG chatbot with tools | Output includes unsupported plugin commands |
| Fintech LLM            | Overgeneration of JSON payloads             |

## Visualization Tools

* LangSmith: prompt tracing, vector deviation
* W\&B Prompts: output scoring vs baselines
* Custom dashboards via Prometheus + Grafana

## Response Strategies

| Strategy           | Action                                    |
| ------------------ | ----------------------------------------- |
| Soft Refusal       | Replace response with denial message      |
| Output Suppression | Discard generation and log incident       |
| Backtrace Logging  | Dump full prompt → output → config        |
| Rate Limiting      | Throttle suspicious users or endpoints    |
| Feedback Loop      | Route anomaly to retraining / RLHF engine |

## Summary

You can’t prevent what you don’t measure.\
Anomaly detection doesn’t stop LLM attacks — it **shows you when they happen**, and **what they look like**.
