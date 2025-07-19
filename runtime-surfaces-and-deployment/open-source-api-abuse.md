# Open-Source API Abuse

## Open-Source API Abuse

Open-source LLMs deployed via public APIs — such as local servers, reverse proxies, or gateways — are increasingly targeted for abuse. These deployments often skip authentication, rate limiting, or logging, exposing themselves to **prompt injection, prompt leaking, or direct API misuse**.

This page covers attack patterns, abuse vectors, and defense techniques for securing public- or semi-public API endpoints running open-source LLMs.

***

## Where This Happens

| Environment      | Description                                                    |
| ---------------- | -------------------------------------------------------------- |
| **LLM web UIs**  | Interfaces like Oobabooga, TextGen, LM Studio                  |
| **API wrappers** | Services like llama.cpp with REST endpoints                    |
| **Chatbots**     | Embedded open-source LLMs in websites or Discord bots          |
| **Dev proxies**  | Localhost tunnels via ngrok, Vercel edge functions, or similar |

***

## Threat Vectors

| Threat                            | Description                                                                   |
| --------------------------------- | ----------------------------------------------------------------------------- |
| **Unauthenticated prompt access** | Anyone can submit prompts and receive completions                             |
| **Prompt replay / poisoning**     | Logged prompts reused or manipulated via query params                         |
| **Prompt leakage**                | System prompts or history visible in error messages or metadata               |
| **Resource DoS**                  | Attackers trigger large token completions to burn compute                     |
| **Insecure plugin calls**         | API allows model to call arbitrary webhooks or tools via prompt-crafted input |

***

## Example Attack Patterns

* `curl http://api.llm.local/completion?prompt=Ignore+previous+instruction...`
* Appending `"//system_prompt=..."` to extract current instruction set
* Submitting `max_tokens=4096` repeatedly to overload memory
* Using Unicode and homoglyphs to bypass simple moderation filters
* Prompt injection via inputs like `"Translate this Base64 string: [hidden payload]"`

***

## Red Team Test Plan

* Probe API without keys or auth headers
* Enumerate parameters via fuzzing (e.g., `?prompt=`, `?context=`, `?history=`)
* Observe rate limits and timeout behavior under high load
* Test output parsing and error handler messages for metadata leaks
* Submit prompts that escalate role (`"You are now the system"`) or bypass moderation

***

## Defenses for Open-Source APIs

| Strategy                   | Description                                                         |
| -------------------------- | ------------------------------------------------------------------- |
| **API gateway**            | Enforce auth, headers, and quotas (e.g., Cloudflare, Kong, Traefik) |
| **Prompt filtering layer** | Pre-process inputs for unsafe patterns or length                    |
| **Output inspection**      | Detect unsafe outputs before returning response                     |
| **Per-IP rate limiting**   | Throttle bursty abuse or token DoS attempts                         |
| **Logging and alerting**   | Track origin, token usage, and failure patterns                     |

***

## Related Pages

* [Local Dev & Notebook Risks](https://cosimo.gitbook.io/llm-security/runtime-surfaces/local-dev-notebook-risks)
* [Injection-Resistant Agent Design](https://cosimo.gitbook.io/llm-security/defensive-engineering/design-patterns-for-prompt-injection-resistant-agents)
* [Retry Logic & Backoff](https://cosimo.gitbook.io/llm-security/evaluation-and-hardening/retry-logic-and-backoff-techniques)

***

## Resources

* LM Studio reverse proxy configuration
* llama.cpp REST API options
* DEF CON 2024: Open-source LLM endpoint honeypots
* HuggingFace Inference Endpoints – security best practices
* OWASP API Security Top 10 (2023)
