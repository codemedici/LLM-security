# LLM Architectures and Deployment Models

Understanding how LLMs are structured and deployed is foundational to assessing their security posture. Different architectures and modalities imply different threat surfaces, attack vectors, and defensive strategies.

## Common Model Architectures

### Decoder-Only Transformers

* Used by GPT, LLaMA, Falcon, Mistral
* Generate outputs token-by-token based on prior context
* Tend to memorize training data more easily

**Security Implication**: More prone to extraction or leakage attacks due to causal attention.

### Encoder-Decoder Transformers

* Used by T5, BART
* Encode input into latent representation and decode into output
* Well-suited for translation, summarization, etc.

**Security Implication**: More complex input/output interaction surface, often safer in some alignment tasks.

### RAG (Retrieval-Augmented Generation)

* Combine a retriever module (e.g., vector store) with a generator (LLM)
* Popular in production chatbots and enterprise search

**Security Implication**: Prone to prompt injection via retrieved documents, file poisoning, and vector attacks.

## Open vs Closed Weight Models

| Type   | Description                            | Examples               |
| ------ | -------------------------------------- | ---------------------- |
| Closed | API access only, weights not available | OpenAI, Anthropic      |
| Open   | Self-hostable, weights available       | LLaMA, Mistral, Falcon |

**Security Implication**:\
Open models increase surface for:

* Weight tampering / trojans
* Backdoor injection
* Insecure inference servers

## Deployment Modalities

### API-Based (Cloud)

* Models hosted by vendors (OpenAI, Claude)
* Accessed via HTTPS + API key
* Includes tools, plugins, agents

**Surface**: Token leaks, API key abuse, plugin injection, prompt chaining.

### On-Premise / Local

* Weights hosted by user
* Inference with Hugging Face, vLLM, TGI, llama.cpp

**Surface**: Model file poisoning, insecure endpoints, lack of telemetry, serialized payloads.

### Edge and Browser-Based

* Small models compiled to run in-browser (WebGPU)
* Deployed to mobile, embedded, or private edge servers

**Surface**: No sandbox, model leakage, weak update control.

## System Architecture Patterns

### Inference Stack

```
[Frontend (Chat UI)]
       ↓
[Backend Router / Proxy]
       ↓
[LLM Inference Server]
       ↓
[Model File + Tokenizer]
```

* Often uses FastAPI, Flask, Docker, Kubernetes
* Plugins/tool use can call subprocesses, APIs, or files

## Real-World Impacts

* Insecure Hugging Face model demos exposing endpoints
* Mislabeled open-source model weights with embedded payloads
* RAG setups serving toxic or malicious content

## Summary

Knowing the architecture of your model and its deployment path is the first step in knowing where to look for vulnerabilities.
