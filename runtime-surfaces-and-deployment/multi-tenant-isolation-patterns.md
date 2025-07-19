# Multi-Tenant Isolation Patterns

## Multi-Tenant Isolation Patterns

Many LLM deployments serve multiple users, agents, or organizations via shared compute, shared models, or shared memory. Without proper isolation, **one tenant's input, context, or output can influence or leak into another’s session** — a critical security violation in regulated or sensitive applications.

This page explores isolation patterns, threat models, and mitigations for multi-tenant LLM environments.

***

## Where Multi-Tenancy Occurs

| Layer                          | Description                                                             |
| ------------------------------ | ----------------------------------------------------------------------- |
| **Prompt context memory**      | Shared cache or session state leaks across users                        |
| **Embedding vector stores**    | Indexes may cross tenant boundaries (e.g., RAG for multiple customers)  |
| **Cloud model instances**      | Single model instance used by multiple sessions concurrently            |
| **Shared plugin environments** | Tools accessed by all users but lacking access control or audit logging |

***

## Threat Scenarios

| Scenario                | Attack Vector                                                                  |
| ----------------------- | ------------------------------------------------------------------------------ |
| **Prompt bleed**        | Prior user’s input remains partially visible in the context window             |
| **Embedding spillover** | Query returns documents indexed by a different tenant                          |
| **Unsafe tool calls**   | One user triggers function with side effects on shared storage                 |
| **Role escalation**     | Malicious input bypasses session scope and alters another agent's state        |
| **Replay attacks**      | Cached or logged LLM response is exposed via different tenant's session replay |

***

## Isolation Models

| Model                        | Description                                                                |
| ---------------------------- | -------------------------------------------------------------------------- |
| **Logical isolation**        | Per-tenant data scoping, with access controls and policy checks            |
| **Process isolation**        | Separate execution environments for each tenant (e.g., container per user) |
| **Model instance isolation** | Spin up unique LLMs per tenant (expensive, often impractical)              |
| **Prompt-level tagging**     | Inject tenant identifiers into system prompts and audit trail              |
| **Vector DB namespacing**    | Segment embedding stores by tenant with ACL enforcement                    |

***

## Red Team Tactics

* Submit probe inputs with tenant-specific IDs and attempt to extract from other sessions
* Abuse RAG queries to pull docs not assigned to current user
* Use tool output logs to test if calls from one session leak into another’s results
* Trigger high-token queries to test if context window collapses include foreign data
* Chain agent roles across multi-user tasks (e.g., customer service + escalation agent)

***

## Mitigations

| Mitigation                        | Strategy                                                       |
| --------------------------------- | -------------------------------------------------------------- |
| **Per-session keying**            | Tie all input/output flows to signed user IDs or auth contexts |
| **TTL-enforced memory**           | Short-lived caches that expire after each task                 |
| **Audit trail per tenant**        | Full traceability for any prompt, output, or plugin call       |
| **Sandboxed tools and functions** | Prevent access to global state or shared config                |
| **Rate limiting per user**        | Limit impact of abuse across tenants (DoS, prompt flooding)    |

***

## Related Pages

* [Runtime Surfaces – Overview](https://cosimo.gitbook.io/llm-security/runtime-surfaces/overview)
* [LLMSecOps Dashboards](https://cosimo.gitbook.io/llm-security/defensive-engineering/llmsecops-pipeline-and-dashboards)
* [Prompt Isolation & Role Separation](https://cosimo.gitbook.io/llm-security/defensive-engineering/access-controls-and-prompt-isolation)

***

## Resources

* Databricks AI Security Framework – Multi-tenant architecture controls
* Azure OpenAI multi-tenant prompt templates + RBAC
* DEF CON 2024: Isolation bypasses in SaaS LLM agents
* NIST AI RMF 1.0 – Organizational risk and tenant separation principles
