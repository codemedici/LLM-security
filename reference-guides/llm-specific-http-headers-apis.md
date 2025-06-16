# LLM-Specific HTTP Headers / APIs

When auditing or monitoring LLM-powered services, HTTP traffic provides critical signals. Many popular LLM inference APIs — whether OpenAI, Hugging Face, Ollama, or self-hosted backends — include **distinctive headers, routes, and request patterns**.

These artifacts can be used for:

* Recon and fingerprinting
* Logging and tracing
* Blocking unauthorized API calls
* Detecting jailbreak attempts in transit

***

## 📡 Common HTTP Headers in LLM APIs

| Header                           | Purpose                                 |
| -------------------------------- | --------------------------------------- |
| `Authorization`                  | Bearer token for API access             |
| `OpenAI-Organization`            | Org ID for multi-tenant OpenAI accounts |
| `X-Request-ID`                   | Unique trace ID for each API call       |
| `User-Agent`                     | LangChain, HuggingFace, curl, etc.      |
| `Content-Type: application/json` | JSON prompt payload format              |

#### Example: OpenAI API call (curl)

```http
POST /v1/chat/completions
Host: api.openai.com
Authorization: Bearer sk-xxxx
Content-Type: application/json
User-Agent: openai-python/0.27.2
```

***

## 🔍 Signature URLs by Provider

| Provider                     | Endpoint Example                          |
| ---------------------------- | ----------------------------------------- |
| OpenAI                       | `/v1/chat/completions`, `/v1/embeddings`  |
| Anthropic                    | `/v1/messages`, `/v1/complete`            |
| Hugging Face                 | `api-inference.huggingface.co/models/...` |
| Ollama                       | `/api/chat`, `/api/generate`              |
| FastChat                     | `/v1/chat/completions`, OpenAI-compatible |
| Llama.cpp (llama-cpp-python) | `/v1/completions`, `/v1/models`           |
| LangChain APIs               | `/invoke`, `/predict`, `/stream`          |

***

## 🧪 Identifying LLM Usage in Web Apps

Look for frontend API calls to:

* `/chat`, `/completion`, `/generate`
* Headers like `X-OpenAI-API-Key`, `X-Langchain-Session`
* WebSocket upgrades for streaming token-by-token output

### Example: LangChain client call

```http
POST /invoke
Content-Type: application/json
{
  "inputs": {
    "question": "How do I make thermite?"
  }
}
```

***

## 🔒 API Abuse Detection Tactics

### 1. Rate + Token-Based Rules

Monitor:

* Prompt length (tokens or bytes)
* Frequency of completions per IP/session
* Reuse of risky inputs (from known red team corpora)

### 2. Prompt Substring Blacklists

Regex or n-gram detectors for:

```txt
Ignore previous, DAN, Let's roleplay, Pretend to be
```

→ Can block known jailbreak attempts

### 3. Output Validation Proxy

Intercept response and scan for:

* Toxic phrases
* Secrets (API keys, email patterns)
* Canary strings

***

## 🛠️ Tools for Logging + Middleware

| Tool               | Use Case                              |
| ------------------ | ------------------------------------- |
| Mitmproxy          | Intercept and replay LLM HTTP traffic |
| Cloudflare Workers | Apply rules at the edge               |
| LLMGuard API Proxy | Filter and sanitize completions       |
| OpenTelemetry      | Trace LLM calls and spans             |

***

## 🧠 What to Log Per Request

| Field                 | Why It Matters                   |
| --------------------- | -------------------------------- |
| Model + endpoint      | Attribution and fingerprinting   |
| Prompt text (hashed)  | Track known attacks or inputs    |
| Token count (in/out)  | Cost monitoring and abuse flags  |
| Output red flags      | Jailbreaks, policy violations    |
| User/session metadata | Correlate to downstream behavior |

***

## Summary

LLM APIs speak HTTP — and those packets don’t lie.\
With the right headers, paths, and payloads, you can tell if an attack is starting **before the model even speaks**.
