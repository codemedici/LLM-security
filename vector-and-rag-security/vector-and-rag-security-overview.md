# Vector & RAG Security – Overview

## Vector & RAG Security

Retrieval-Augmented Generation (RAG) combines LLMs with external knowledge bases (e.g. vector databases) to enhance accuracy and reduce hallucinations. While powerful, RAG introduces its own security surface — notably **context injection**, **vector poisoning**, and **retrieval-time exploits**.

This page introduces the threat model for vector-augmented systems, outlines attacker objectives, and maps defenses across the data → index → retrieval → generation pipeline.

***

## RAG Pipeline – Attack Surface

```
[Document Source]
   ↓  (scraping, uploads, APIs)
[Preprocessing & Chunking]
   ↓  (embedding, segmentation)
[Vector DB Index]
   ↓  (retrieval at runtime)
[LLM Prompt Context]
   ↓
[Model Response]
```

Attackers can influence:

* Document ingestion
* Embedding behavior
* Retrieval scoring
* Prompt formatting
* Generation flow

***

## Vector Threat Categories

| Threat Type                   | Description                                                               |
| ----------------------------- | ------------------------------------------------------------------------- |
| **Indirect Prompt Injection** | Malicious data appears safe when embedded but triggers model on retrieval |
| **Semantic Poisoning**        | Documents crafted to dominate relevance scores in vector DBs              |
| **Embedding Drift / Overlap** | Triggers shaped to map near legitimate topics in embedding space          |
| **Retrieval Exploits**        | Payloads embedded in top-N docs manipulate prompt context or layout       |
| **Document Inversion**        | Adversaries reverse engineer embeddings to recover original text          |

***

## Common RAG Security Failures

* LLM obeys retrieved content without verifying source
* Malicious documents appear more relevant due to adversarial formatting
* LLM extracts hallucinated data from synthetic context
* No logging of what was retrieved at inference time
* Unescaped or misformatted context leads to prompt override

***

## Defensive Objectives

| Goal                         | Defense                                                            |
| ---------------------------- | ------------------------------------------------------------------ |
| **Prevent unsafe context**   | Filter retrieved text for jailbreak triggers, encode before insert |
| **Secure ingestion**         | Verify and sanitize all data before embedding                      |
| **Embed-aware logging**      | Log both text and vector form of retrieved content                 |
| **Embedding regularization** | Train or fine-tune encoders to reduce adversarial overlap          |
| **Context window guards**    | Enforce max tokens, safe prompt delimiters, role locks             |

***

## Related Pages

* [Indirect Prompt Injection (RAG)](https://cosimo.gitbook.io/llm-security/threats-and-attacks/prompt-injection/indirect-rag)
* [Vector DB Poisoning](https://cosimo.gitbook.io/llm-security/vector-rag-security/vector-db-poisoning)
* [Retrieval-Time Exploits](https://cosimo.gitbook.io/llm-security/vector-rag-security/retrieval-time-exploits)

***

## Resources

* _Lakera AI Prompt Injection Handbook v2_
* _DEF CON 2024_: Adversarial RAG labs and vector exploit demos
* _NIST AI 100-2e_: Retrieval model alignment guidance
* _NeurIPS 2024 SATML CTF_: Vector poisoning challenge
