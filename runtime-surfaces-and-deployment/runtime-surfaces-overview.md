# Runtime Surfaces - Overview

## Runtime Surfaces – Overview

The deployment context of an LLM — cloud API, on-prem cluster, edge device, or notebook — defines its runtime threat surface. While most security guidance focuses on models and prompts, **many real-world exploits occur at the deployment and integration layer**.

This section maps the most critical runtime surfaces and presents adversarial perspectives, attack vectors, and hardening strategies across each environment.

***

## Key Deployment Contexts

| Context                                | Examples                                                |
| -------------------------------------- | ------------------------------------------------------- |
| **Cloud / SaaS LLM APIs**              | OpenAI, Anthropic, Mistral, Google Gemini, Azure-OpenAI |
| **Open-source LLM on VM or container** | llama.cpp, Ollama, LMDeploy, vLLM                       |
| **Enterprise LLM gateways**            | LangChain, DSPy, Azure ML endpoints                     |
| **Multi-agent orchestration**          | CrewAI, AutoGen, AutoGPT                                |
| **Notebook / local prototyping**       | Jupyter, Google Colab, VSCode                           |
| **Edge inference**                     | Jetson, mobile, WebAssembly + WASM LLMs                 |

***

## Threat Surfaces at Runtime

| Layer                       | Example Threats                                                |
| --------------------------- | -------------------------------------------------------------- |
| **API exposure**            | Prompt injection → plugin call → external API abuse            |
| **File system access**      | LLMs writing/reading from disk via wrappers                    |
| **Credential leakage**      | Keys exposed via config or prompt-generated outputs            |
| **Multi-user memory bleed** | Shared cache revealing other tenants’ prompts                  |
| **Token overflow**          | Long input + long context = eviction of safety or role prompts |
| **Sandbox breakout**        | Execution via tools or eval() in insecure plugins              |

***

## Risk Themes

* **Implicit trust in agent wrappers**
* **Token-based billing abuse**
* **Weak isolation in serverless contexts**
* **Unbounded tool/plugin execution**
* **State leakage across requests**

***

## Defensive Priorities

| Surface                     | Mitigation                                                          |
| --------------------------- | ------------------------------------------------------------------- |
| **Plugin execution**        | Limit permissions, enforce output schemas, sandbox                  |
| **Memory & cache**          | Use per-user and per-session scoping, TTLs, and role revalidation   |
| **Prompt routing**          | Never pass raw user input into system prompts                       |
| **Environment hardening**   | Disable `os`, `eval`, file I/O in plugin functions                  |
| **Logging & observability** | Log tool calls, prompt deltas, and model switchovers with trace IDs |

***

## Related Pages

* [Cloud / SaaS Platforms](https://cosimo.gitbook.io/llm-security/runtime-surfaces/cloud-saas-platforms)
* [Multi-Tenant Isolation Patterns](https://cosimo.gitbook.io/llm-security/runtime-surfaces/multi-tenant-patterns)
* [Local Dev & Notebook Risks](https://cosimo.gitbook.io/llm-security/runtime-surfaces/local-dev-notebook-risks)

***

## Resources

* Databricks AI Security Framework (DASF) v4
* Anthropic Claude plugin execution policies (System Cards)
* DEF CON 2024: LLM Deployment Security Workshop
* OpenAI Platform Docs – Runtime hooks and function schemas
* NIST AI 100-2e: “Secure Deployment” and infrastructure isolation principles
