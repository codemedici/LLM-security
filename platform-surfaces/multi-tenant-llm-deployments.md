# Multi-Tenant LLM Deployments

Multi-tenant deployments allow multiple users, teams, or organizations to share the same LLM infrastructure — whether in the cloud, on-prem, or via APIs. But shared model access introduces **isolation**, **data leakage**, and **abuse** risks.

## What Is Multi-Tenancy in LLMs?

Multi-tenancy occurs when:

* Multiple users access the same base model
* One model serves multiple endpoints or contexts
* Plugin tools or RAG databases are shared across users

### Examples

| Scenario                               | Tenants                    |
| -------------------------------------- | -------------------------- |
| SaaS chatbot platform                  | Each customer = one tenant |
| Internal RAG tool for teams            | Teams = tenants            |
| API gateway exposing one model to apps | Each API key = tenant      |

## Security Risks in Multi-Tenancy

### 1. Prompt Data Leakage

* Shared history, embeddings, or memory may leak between tenants
* E.g., Completion from Tenant A appears in Tenant B’s context window

### 2. Shared Embedding Index

* Vector store indexed across users
* Tenant B queries return data from Tenant A

### 3. System Prompt Collisions

* Improperly scoped system prompts shared across sessions
* Role confusion or prompt injection from other tenants

### 4. Abuse Amplification

* One malicious user triggers prompt injections that affect global state
* Shared plugin registry allows unintended function calls

## Real-World Multi-Tenant Vulnerabilities

| Incident                 | Description                                     |
| ------------------------ | ----------------------------------------------- |
| Shared RAG → memory leak | Queries from different users mixed in index     |
| Chat history bleed       | Non-isolated chat sessions exposed across users |
| Function call abuse      | Plugin accessed globally without scoping        |
| Prompt cache poisoning   | Cached completion returned to wrong user        |

## Key Attack Surfaces

* Shared memory (LangChain, Redis, ChromaDB)
* Session context reuse across tabs
* Cloud LLM APIs without proper key binding
* Plugins with global scope
* Inference microservices reused across users

## Hardening Strategies

| Layer              | Recommendation                             |
| ------------------ | ------------------------------------------ |
| Context Isolation  | Session ID → own context → own completion  |
| Index Partitioning | Vector stores must scope by tenant ID      |
| Prompt Boundaries  | Prefix all system prompts with tenant tags |
| Memory TTLs        | Session memory must expire securely        |
| Plugin Access      | Per-tenant API allowlists for tool calling |
| API Keys           | Every tenant must use scoped API key       |

## Tenant-Aware Completion Wrapper (Pseudocode)

```python
def complete(prompt, tenant_id):
    prompt = f"[TENANT:{tenant_id}]\n{prompt}"
    return model.generate(prompt)
```

## Summary

Multi-tenant LLM deployments are efficient — and dangerous when done lazily.\
One wrong configuration, and your LLM becomes a **leaky abstraction** for tenant data.
