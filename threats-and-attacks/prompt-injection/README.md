---
description: >-
  Overview of prompt injection vulnerabilities in LLMs, including direct,
  indirect (RAG-based), and multi-hop attacks.
---

# Prompt Injection

## Prompt Injection – Overview

Prompt injection is one of the most pervasive and high-impact vulnerabilities in large language model (LLM) applications. It involves manipulating the input prompt such that the model produces unintended behavior, often by overriding prior instructions or injecting malicious payloads.

This attack class is increasingly dangerous due to the rapid adoption of LLMs in software pipelines, chat interfaces, agents, and retrieval-augmented generation (RAG) workflows. It is ranked **#1 in the OWASP Top 10 for LLM Applications**.

Prompt injection attacks vary in sophistication and target context, ranging from simple overrides to multi-stage exploit chains. The following subpages provide in-depth analysis of:

* [Direct Prompt Injection](https://chatgpt.com/g/g-p-686fcdd11388819199552779068fc4c1-ai-red-teaming-notebook/c/direct.md): Inserting malicious content into the prompt directly.
* [Indirect Prompt Injection / RAG](https://chatgpt.com/g/g-p-686fcdd11388819199552779068fc4c1-ai-red-teaming-notebook/c/indirect-rag.md): Exploiting RAG pipelines by injecting payloads into source documents.
* [Multi-Hop & Cross-App Injection](https://chatgpt.com/g/g-p-686fcdd11388819199552779068fc4c1-ai-red-teaming-notebook/c/multi-hop-cross-app.md): Chaining injections across apps, memory, or agents.

### Real-World Risk

Prompt injection has been observed in:

* Customer support agents
* Code generation tools
* Email assistants
* Financial bots
* AI-integrated plugins and function-calling apps

Attackers have leveraged these issues for:

* Data exfiltration
* Policy evasion
* Prompt leakage
* Cross-user data access

### Anatomy of a Prompt Injection

Prompt injections typically take advantage of one or more of the following:

* **Prompt concatenation** without proper boundary control or role separation
* **Untrusted inputs** embedded into the prompt without sanitization
* **Blind trust** in natural language commands or external data sources

### Mitigation Strategies (Brief)

See the [Defensive Engineering](https://chatgpt.com/g/defensive-engineering/overview.md) section for details.

* Use prompt isolation and structured input templates
* Sanitize user and RAG inputs
* Implement output filters and response classification
* Apply LLM-specific role separation where supported

### Further Reading

* [OWASP Top 10 for LLM Applications](https://owasp.org/www-project-top-10-for-large-language-model-applications/)
* Lakera AI: Prompt Injection Attacks Handbook
* Red Teaming AI by Dursey (Ch. 8, 14)
* SATML CTF (NeurIPS 2024): Lessons from live prompt injection exploit challenges
