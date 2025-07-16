# LLM Architectures and Deployment Models

## LLM Architectures and Deployment Models

Understanding how LLMs are structured and deployed is foundational to assessing their security posture. Different architectures and deployment modalities expose different **threat surfaces**, **attack vectors**, and require distinct **defensive strategies**.

***

### 🔧 Common Model Architectures

#### Decoder-Only Transformers

* **Examples:** GPT, LLaMA, Falcon, Mistral
* **Function:** Generate outputs token-by-token using causal attention
* **Use Case:** Chatbots, completion, summarization

**🔐 Security Implications:**

* Memorize data more easily → prone to **training data leakage**, **membership inference**, **model inversion**
* Vulnerable to **prompt injection**, **token bias manipulation**

***

#### Encoder-Decoder Transformers

* **Examples:** T5, BART, mT5
* **Function:** Encode input to a latent space, then decode
* **Use Case:** Translation, summarization, text rewriting

**🔐 Security Implications:**

* Better input/output separation, may reduce attack surface in some tasks
* But complexity opens risk to **input-overflow, output-hallucination**, or **alignment mismatch**

***

#### Retrieval-Augmented Generation (RAG)

* **Examples:** ChatGPT w/ Browsing, LangChain agents, enterprise Q\&A bots
* **Function:** Augments model with external knowledge from vector DBs
* **Use Case:** Knowledge grounding, document Q\&A, legal/financial summarization

**🔐 Security Implications:**

* **Indirect prompt injection** via documents or indexed content
* Vector DBs vulnerable to **poisoning**, **embedding attacks**, and **untrusted inputs**

***

### 🔓 Open vs. Closed Weight Models

| Model Type | Description                       | Examples               | Security Implications                                                                          |
| ---------- | --------------------------------- | ---------------------- | ---------------------------------------------------------------------------------------------- |
| Closed     | API-only access; hosted by vendor | OpenAI, Anthropic      | Data protected, but **opaque behavior** and **API key leakage risk**                           |
| Open       | Self-hosted; weights downloadable | LLaMA, Mistral, Falcon | Exposes attack surface: **model tampering**, **trojaned weights**, **RCE via custom handlers** |

Open-weight models require **supply chain security**, **weight verification**, and **container isolation** to reduce risk.

***

### 🌐 Deployment Modalities

#### API-Based / Cloud-Hosted

* **Usage:** Call OpenAI, Claude, Gemini via HTTPS
* **Integration:** Often part of tools, plugins, agents

**⚠️ Threats:**

* API key leakage
* Token-level exfiltration
* Plugin misuse
* Poor rate-limiting or isolation between users

***

#### On-Premise / Self-Hosted

* **Tools:** vLLM, TGI, Hugging Face, llama.cpp
* **Used For:** Full control, fine-tuning, privacy

**⚠️ Threats:**

* **Insecure endpoints** (localhost or Flask)
* **Pickle deserialization** backdoors
* **Model file poisoning**
* **No audit/logging telemetry by default**

***

#### Edge, Browser-Based, Embedded

* **Examples:** WebLLM (WebGPU), llama.cpp mobile, quantized tiny LLMs
* **Deployment:** On-device inference (no external calls)

**⚠️ Threats:**

* No sandbox → direct access to model weights
* Users can extract parameters or manipulate update logic
* **No remote kill switch** or policy updates once deployed

***

### 🧱 LLM System Architecture Pattern

```plaintext
[Frontend (Chat UI)]
        ↓
[Router / Orchestrator / API Gateway]
        ↓
[LLM Inference Engine (vLLM, TGI)]
        ↓
[Model Weights + Tokenizer + Tools]
```

* Plugins or tools may trigger subprocesses, fetch URLs, or invoke shell commands
* Every component is **a security boundary** that must be hardened independently

***

### 🧪 Real-World Security Incidents

* 🔓 \[Hugging Face Spaces] deployed with unprotected inference endpoints
* 🐛 LLaMA-based models backdoored via malicious safetensors or Pickle files
* 📚 RAG apps serving unsafe instructions from poisoned PDFs
* ⚙️ LangChain agents accidentally triggering OS-level commands

***

### ✅ Summary

> **Understanding your model's architecture and deployment path is the first step to defending it.**

Each choice — model type, weight access, or deployment stack — reshapes the **attack surface** and demands different **mitigation strategies**:

* Trust boundaries shift with tools and plugins
* Observability varies between open vs. closed systems
* Edge and local deployments need stronger supply chain hygiene
