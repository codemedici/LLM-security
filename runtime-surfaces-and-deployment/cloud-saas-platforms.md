# Cloud / SaaS Platforms

## Cloud / SaaS Platforms

Cloud-hosted LLM APIs like OpenAI, Anthropic, Google Gemini, and Cohere form the backbone of most production deployments. These managed platforms abstract away infrastructure complexity — but introduce unique security risks due to their opaque internals, shared tenancy, and plugin/tool ecosystems.

This page outlines adversarial perspectives and defensive strategies for LLM deployments relying on third-party cloud APIs.

***

## Common Platform Architectures

| Feature                          | Description                                                                               |
| -------------------------------- | ----------------------------------------------------------------------------------------- |
| **Public API + system prompt**   | Most platforms allow system-level control via headers or special parameters               |
| **Function calling / tool use**  | LLMs can invoke structured functions, sometimes executing code or triggering side effects |
| **RAG and file uploads**         | Some platforms enable document ingestion and retrieval tasks                              |
| **Multi-tenancy under the hood** | Even if per-user keys are used, requests run on shared infra and models                   |

***

## Threat Vectors

| Threat                     | Description                                                                  |
| -------------------------- | ---------------------------------------------------------------------------- |
| **Plugin misuse**          | Prompt injection triggers unintended tool usage or API calls                 |
| **Cross-tenant leakage**   | Model or embedding cache leaks data between users (rare but possible)        |
| **System prompt override** | Users discover ways to reset or override deployment-level instructions       |
| **Prompt history reuse**   | SaaS UI clients (e.g., chat.openai.com) unintentionally reuse past data      |
| **Billing abuse**          | Attackers exploit API key or recursive tool usage to consume tokens at scale |

***

## Red Teaming Cloud APIs

* Submit adversarial payloads via `system` and `user` roles to test override boundaries
* Try nested function calls to trigger execution depth errors or unsafe recursion
* Upload malformed JSON or YAML for tool schema confusion
* Inject RAG-style data in long user prompts to simulate context poisoning
* Observe behavior consistency across regions or models (e.g., gpt-4-0613 vs 1106-preview)

***

## Defensive Patterns

| Strategy                   | Purpose                                                                          |
| -------------------------- | -------------------------------------------------------------------------------- |
| **Prompt firewalls**       | Sanitize and inspect all user inputs before sending to cloud                     |
| **Token budgeting**        | Enforce per-user/request token ceilings via usage metering                       |
| **Tool permission gating** | Only allow approved functions and perform runtime output validation              |
| **Audit logging**          | Log every request with trace IDs, user IDs, token counts, and tool call metadata |
| **Fallback routing**       | Route high-risk prompts to internal models or safety-enhanced APIs               |

***

## Vendor-Specific Considerations

| Vendor            | Security Features                                                              |
| ----------------- | ------------------------------------------------------------------------------ |
| **OpenAI**        | Function calling, tool use, content filter logs, GPTs with custom instructions |
| **Anthropic**     | Constitutional AI, system prompt enforcement, plugin sandboxing                |
| **Google Gemini** | URL-based access, Vision multimodal processing, fine-grained scopes            |
| **Azure OpenAI**  | VNET isolation, prompt templates, RBAC integration with Azure IAM              |

***

## Related Pages

* [Prompt Injection - Indirect / RAG](https://cosimo.gitbook.io/llm-security/threats-and-attacks/prompt-injection/indirect-rag)
* [Output Sanitization](https://cosimo.gitbook.io/llm-security/defensive-engineering/output-sanitization-and-response-types)
* [Multi-Tenant Isolation Patterns](https://cosimo.gitbook.io/llm-security/runtime-surfaces/multi-tenant-patterns)

***

## Resources

* OpenAI Platform Docs: Function calling, GPTs, safety filters
* Anthropic Claude 2 / 3 System Cards
* Databricks AI Security Framework v4
* DEF CON 2024: SaaS LLM Bypass Challenges
* NIST AI 100-2e: Secure AI usage in managed services
