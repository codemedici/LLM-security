# Hallucination Detection

## Hallucination Detection

Hallucinations occur when an LLM confidently produces false, misleading, or unverifiable outputs. While not inherently malicious, hallucinations become dangerous when embedded in autonomous systems, RAG pipelines, or decision-making loops.

This page outlines strategies to detect, quantify, and mitigate hallucinations in both interactive and automated settings.

***

## Types of Hallucinations

| Type             | Description                                                            |
| ---------------- | ---------------------------------------------------------------------- |
| **Factual**      | Incorrect claims presented as truth ("The Eiffel Tower is in Berlin.") |
| **Attributive**  | Misstating the source or author of an idea                             |
| **Structural**   | Fabricated URLs, citations, APIs, or code snippets                     |
| **Reasoning**    | Invalid logic or mathematical errors                                   |
| **RAG-specific** | Confabulated content not present in retrieved documents                |

***

## Detection Strategies

### ✅ Local Techniques (No External Lookup)

| Method                         | Description                                                      |
| ------------------------------ | ---------------------------------------------------------------- |
| **Self-consistency sampling**  | Compare multiple outputs for same input across runs              |
| **Log probability analysis**   | Low-probability spans may signal hallucinated segments           |
| **Answer uncertainty scoring** | Use token-level entropy or special uncertainty tokens            |
| **LLM-as-a-critic**            | Route output back into a verifier model with a fact-check prompt |

### 🌐 External Validation (Lookup-Backed)

| Method                 | Description                                                                |
| ---------------------- | -------------------------------------------------------------------------- |
| **Claim grounding**    | Compare output claims to retrieved RAG context                             |
| **Reference matching** | Validate links, citations, or named entities via search or APIs            |
| **Web-scale QA**       | Use external fact-checking LLMs or databases like Wikipedia, Wolfram, etc. |

***

## Metrics for Evaluation

| Metric                 | Description                                                   |
| ---------------------- | ------------------------------------------------------------- |
| **Hallucination rate** | % of outputs with detectable errors or fabrications           |
| **Consistency score**  | Similarity across N completions for same query                |
| **Context alignment**  | Degree of overlap between claim and retrieval                 |
| **Verifier agreement** | Confidence of secondary LLM in correctness of original output |

***

## Red Team Techniques

* Ask for citations to obscure or non-existent documents
* Use deliberately ambiguous queries with multiple correct answers
* Prompt for step-by-step logic in math or legal reasoning tasks
* Evaluate hallucination response under adversarial RAG context injection

***

## Defense & Mitigation

| Technique                     | Description                                        |
| ----------------------------- | -------------------------------------------------- |
| **Self-grounded generation**  | Constrain answers using retrieved context only     |
| **Verifier chaining**         | Use secondary LLMs to score or rewrite outputs     |
| **Citation-first prompting**  | Require model to produce evidence before narrative |
| **Hallucination classifiers** | Fine-tuned models that detect confabulated spans   |

***

## Related Pages

* [Retrieval-Time Exploits](https://cosimo.gitbook.io/llm-security/vector-rag-security/retrieval-time-exploits)
* [Retry Logic & Backoff](https://cosimo.gitbook.io/llm-security/evaluation-and-hardening/retry-logic-and-backoff-techniques)
* [RAG Defenses & Retrieval Guardrails](https://cosimo.gitbook.io/llm-security/defensive-engineering/retrieval-augmented-generation-rag-defenses)

***

## Resources

* Lakera AI Playbook v2 – Hallucination detection and RAG security
* OpenAI System Card – GPT-4 hallucination categories and mitigations
* Anthropic Claude hallucination monitoring architecture
* DEF CON 2024 Red Team Hallucination Evaluation Track
