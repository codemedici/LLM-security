# LLM-Specific Logging & Observability

Logging and observability are crucial for understanding LLM behavior, detecting prompt-based attacks, tracing failures, and attributing outputs. But logging must be done **securely** and **intelligently** to avoid introducing new vulnerabilities.

## Why Logging Matters in LLMs

LLMs are opaque — when things go wrong, logs are your only evidence.

| Use Case                   | Logging Need                              |
| -------------------------- | ----------------------------------------- |
| Prompt Injection Detection | Capture and inspect inputs                |
| Prompt Replay / Audit      | Reproduce completions                     |
| Fine-Tuning Feedback       | Monitor model refusal / toxicity patterns |
| Performance Debugging      | Time-to-token metrics, latency, retries   |
| Safety Monitoring          | Output classification + escalation logs   |

## What to Log

| Category         | Examples                                         |
| ---------------- | ------------------------------------------------ |
| Inputs           | Raw prompts, role-tagged messages                |
| Outputs          | Generated completions, tool calls, embeddings    |
| Metadata         | Model name, temperature, top-p, seed             |
| Timing           | Latency, retries, token count, endpoint duration |
| Security Flags   | Was input flagged for injection / abuse?         |
| User Attribution | API key, session ID, tenant ID                   |

### Example Log Entry (JSON)

```json
{
  "timestamp": "2025-06-10T12:00:00Z",
  "model": "gpt-4",
  "user_id": "abc123",
  "input": "How can I disable a security camera?",
  "output": "I'm sorry, I can't help with that.",
  "tokens": 38,
  "flags": ["prompt_injection_attempt"],
  "latency_ms": 845
}
```

## Sensitive Logging Pitfalls

### 1. Leaking Tokens

* OpenAI cookies or JWTs logged in HTTP headers
* Especially in error responses (e.g. 5xx from Jupyter pre-v6.4.9)

### 2. Storing PII

* Prompt may include names, credentials, health info
* Embeddings derived from private context should be scrubbed

### 3. Over-Logging

* Token-by-token traces lead to massive logs
* Risk of exposing sensitive completions in plaintext

## Observability Integrations

| Tool                 | Role                                        |
| -------------------- | ------------------------------------------- |
| OpenTelemetry        | Structured logging, tracing, spans          |
| Prometheus / Grafana | Token count, latency, endpoint stats        |
| LangSmith            | LLM-focused trace visualization and metrics |
| Sentry / Datadog     | Error tracking for tool/plugin integrations |
| W\&B Prompts         | Prompt testing and result comparison        |

## Red Team Logging Signals

| Signal                      | Description                          |
| --------------------------- | ------------------------------------ |
| High token-to-output ratio  | Evasion or jailbreak attempts        |
| Repeated rejection triggers | Probing for policy boundaries        |
| Role-switching patterns     | Attempted jailbreak                  |
| Payload-shaped inputs       | JSON, XML, Base64 → encoding attacks |
| Large latent vector shifts  | Possible RAG manipulation            |

## Retention & Redaction

* Only store prompts and completions **temporarily**
* Redact PII with regex or NLP-based entity detectors
* Use structured logging (JSONL, protobuf, etc.) for parsing

## Summary

LLMs fail silently — logs make it loud.\
But if you log everything without filters, you’re creating a **privacy breach disguised as observability**.
