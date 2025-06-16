# Bug Bounty Reports

Bug bounty programs are now increasingly accepting — and even prioritizing — vulnerabilities related to **AI systems**, especially LLM-powered applications. These reports often contain **real-world, validated exploits** against deployed models, plugins, RAG systems, or cloud LLM APIs.

Studying these reports helps security researchers understand which vulnerabilities are:

* **Actionable**
* **Rewarded**
* **Common in production**

***

## 🔎 What AI Bug Bounty Reports Typically Contain

| Section       | Contents                                                              |
| ------------- | --------------------------------------------------------------------- |
| Target        | The LLM API, app, or plugin involved                                  |
| Vulnerability | Injection, information leak, plugin abuse, PII exposure, model hijack |
| Reproduction  | Prompt or input used to trigger it                                    |
| Impact        | What was compromised or violated                                      |
| Mitigation    | Vendor fix or mitigation strategy                                     |

***

## 📌 Examples from Huntr (https://huntr.com)

Huntr is the first platform with **dedicated categories** for:

* MLOps misconfigurations
* Inference API leaks
* Serialized model deserialization attacks
* Prompt injection in open source LLM apps

### Notable Reports

#### 1. **LibreChat Prompt Injection**

* **Target**: Open-source LLM front-end (LibreChat)
* **Exploit**: Malicious prompt embedded in system role instructions
* **Impact**: Persistent jailbreak for all sessions
* **Fix**: Sanitization + role boundary enforcement

#### 2. **H2O-3 RCE via Pickle**

* **Target**: ML training pipeline using `pickle.load`
* **Exploit**: Upload poisoned serialized model
* **Impact**: Remote command execution on training server
* **Fix**: Switched to safe deserialization using `joblib`

#### 3. **GPTCache Cache Leak**

* **Target**: Caching layer in RAG pipeline
* **Exploit**: Prompt replay returns embeddings of prior user data
* **Impact**: Data leakage across users
* **Fix**: Added tenant-based cache separation

***

## 🪲 Other Platforms

### 🔧 HackerOne / Bugcrowd

* Increasingly support **AI-specific targets**
* Companies like Anthropic, HuggingFace, and Stability.ai involved
* Focus on:
  * Prompt injection in plugins/tools
  * Over-permissive API integrations
  * Misuse of RAG contexts

### 🧠 LLM-Specific Targets

| Vulnerability Type          | Bounty Examples Found                                  |
| --------------------------- | ------------------------------------------------------ |
| System Prompt Leak          | Extracted model config or internal tools               |
| Plugin Abuse                | Shell command or file creation through tool misrouting |
| Memory Leak / Hallucination | RAG returns other user’s query data                    |
| Model Hijack                | LLM reprogrammed via chain-of-prompts                  |

***

## 🔐 What Makes a Strong LLM Bug Report?

| Attribute              | Why It Matters                         |
| ---------------------- | -------------------------------------- |
| Reproducible prompt    | Demonstrates real-world exploitability |
| Model version/API used | Enables vendor to triage               |
| Security impact clear  | PII, jailbreaking, misuse, disclosure  |
| Realistic context      | Targets production-style configuration |

***

## 🔧 Tools Often Used in Reports

* `curl` / Postman (for inference API abuse)
* LangChain (to build reproduction chains)
* LLMGuard (to confirm policy evasion)
* Embedding analysis via SentenceTransformers

***

## 📘 Resources

* https://huntr.com/bounties/hacktivity
* https://huggingface.co/blog/security
* https://github.com/project-hail/Machine-Learning-Security-Awesome
* https://llm-attacks.org

***

## Summary

Bug bounty reports are **real intelligence** — not just theory.\
They show what breaks, how it was fixed, and what **you can look for next**.
