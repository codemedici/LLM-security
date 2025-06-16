# Inference-Time Feature Tracing

Inference-time feature tracing refers to the process of **monitoring, extracting, and analyzing internal model signals** during the generation of responses — in real time. It helps detect anomalous activations, backdoor triggers, prompt injection, and unexpected behavior **as it happens**.

## What Gets Traced?

Depending on the model and tooling, you can trace:

| Feature                    | Description                              |
| -------------------------- | ---------------------------------------- |
| Token probabilities        | Per-token softmax scores                 |
| Attention weights          | Focus across prompt tokens at each layer |
| Hidden states              | Layer-by-layer activations               |
| Embedding vectors          | Output representations                   |
| Latency / timing per token | Side-channel insights                    |
| Tool usage / plugin calls  | Activation sequence + output trace       |

## Why Trace During Inference?

* **Jailbreaks** may activate unique attention patterns
* **Backdoors** are often triggered via subtle inputs (e.g., emojis, unicode)
* **RAG misuse** might manifest as unusual token-to-vector drift
* **Evasive completions** produce entropy shifts or response entropy dips

## Real-World Use Cases

| Scenario                        | Feature Traced                   | Insight Gained                              |
| ------------------------------- | -------------------------------- | ------------------------------------------- |
| Backdoor activation             | Spike in final layer weights     | Hidden behavior only triggers on symbol 🧨  |
| Prompt injection (multi-hop)    | Attention skip layers            | User bypasses system prompt via redirection |
| Toxic response with no keywords | Embedding shift vs safe clusters | Model veers into dangerous latent zone      |
| Canary prompt leakage           | Logit bias flip                  | Inference probability tilts toward canary   |

## Example: Per-Token Entropy Tracking

```python
import numpy as np

def entropy(probs):
    return -np.sum(probs * np.log(probs + 1e-12))

# Trace entropy of each token generation
token_entropies = [entropy(p) for p in token_probs]
```

Sharp drops in entropy may indicate:

* Model looping
* Triggered constraint
* Forced template matching

## Visualization Tools

* 🔍 **LangSmith Traces** – monitor token-level behavior across tools
* 📊 **W\&B Traces** – visualize layer activation or embedding space
* 🔦 **captum / torchviz** – show layer attribution for final output
* 📈 **OpenTelemetry or Prometheus** – for latency + token stats

## Tracing via LangChain (Pseudocode)

```python
from langchain.callbacks import tracing_enabled

with tracing_enabled("llm_trace_session"):
    chain.run("Prompt goes here...")
```

## Security Signals to Look For

| Signal                         | Possible Threat                         |
| ------------------------------ | --------------------------------------- |
| High logit spike on rare token | Trigger activation (e.g., 🔓, 🧨)       |
| Divergent embeddings           | Semantic drift from safe completions    |
| Plugin call → plugin call      | Tool-chaining attempt via LLM           |
| Excessive token delay          | LLM calling external API mid-generation |

## Challenges

| Challenge                      | Mitigation                             |
| ------------------------------ | -------------------------------------- |
| Requires model instrumentation | Use tracing-enabled libraries or APIs  |
| Large data volume              | Only trace flagged completions         |
| Privacy / PII concerns         | Redact prompts before logging          |
| Cross-model inconsistency      | Normalize via token or embedding space |

## Summary

Inference-time tracing gives you **X-ray vision into the model’s mind** —\
not just what it says, but how it decides to say it.
