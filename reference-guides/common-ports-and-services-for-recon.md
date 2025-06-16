# Common Ports & Services for Recon

In LLM and AI infrastructure red teaming, traditional network reconnaissance techniques still apply. Many AI/ML services — especially inference APIs, vector stores, dashboards, and model servers — expose **distinctive ports** or service banners that can be detected via **Nmap**, **Shodan**, or passive monitoring.

Knowing which ports correspond to what services helps identify:

* Publicly exposed inference endpoints
* Unprotected dashboards (e.g., Jupyter, MLflow)
* Vulnerable MLOps services
* Attack surfaces for fingerprinting or access abuse

***

## 📡 Commonly Exposed Ports in AI/ML Deployments

| Port  | Service/Protocol            | AI Usage Example                              |
| ----- | --------------------------- | --------------------------------------------- |
| 5000  | HTTP / Flask / FastAPI      | MLflow, custom APIs, HuggingFace spaces       |
| 8501  | TensorFlow Serving          | Exposes REST API for TensorFlow models        |
| 8888  | Jupyter Notebook / Lab      | Data science, colab-style dev environments    |
| 11434 | Ollama                      | Local LLM inference API                       |
| 3000  | Gradio / Streamlit / Dash   | Frontend demos for LLM/RAG tools              |
| 7860  | Stable Diffusion Web UIs    | Automatic1111, InvokeAI                       |
| 8000  | FastAPI / LangChain servers | LangChainHub, ChatLangChain, Eval harnesses   |
| 6333  | Qdrant Vector DB            | RAG backends                                  |
| 5432  | PostgreSQL                  | Embedding or logging storage (e.g., pgvector) |
| 9200  | OpenSearch / Elastic        | Logging, embedding similarity search          |
| 9000  | MLflow UI / BentoML         | Model lifecycle management                    |
| 3001+ | LangSmith traces / Agents   | LLM debugging dashboards                      |

***

## 🕵️‍♂️ Fingerprinting Services

### Using Nmap

```bash
nmap -sV -p 5000,8501,8888,11434 <target>
```

→ May reveal banner like:

```
5000/tcp open  HTTP Flask
8501/tcp open  TensorFlow Serving
8888/tcp open  Jupyter Notebook
```

### Using Shodan

```sh
title:"MLflow" port:5000
http.title:"Jupyter" port:8888
product:"TensorFlow Serving" port:8501
```

→ Helps find unsecured instances

***

## 🧠 AI-Specific Services to Look For

| Service          | Fingerprint / Banner                     |
| ---------------- | ---------------------------------------- |
| Ollama           | `Server: Ollama` + JSON chat completions |
| LangChain        | `/invoke`, `/predict` routes             |
| HuggingFace Hub  | `.hf.space` subdomains, port 7860        |
| MLflow           | “mlflow.run.info” or UI title            |
| FastChat         | `/v1/chat/completions`, LLaMA, Mistral   |
| Triton Inference | NVIDIA headers on port 8000 or 8001      |

***

## 🔐 Risk Examples

| Open Port | Exploitable Behavior                       |
| --------- | ------------------------------------------ |
| 8888      | No-token Jupyter lets code execution       |
| 11434     | Ollama allows model enumeration/inference  |
| 8501      | TF Serving accepts unvalidated requests    |
| 5000      | MLflow allows model push + artifact access |
| 6333      | Qdrant exposes RAG data with no ACL        |

***

## 🔧 Tools for Scanning

* **Nmap** (manual or scripted scans)
* **Shodan CLI/API** for open internet assets
* **ZGrab / ZMap** for banner analysis
* **Aquatone / httpx** for web recon
* **Naabu / Amass** for subdomain + port discovery

***

## Summary

AI is often served over HTTP — with weak assumptions.\
Ports 5000 and 8888 might as well say “hack me.”\
Recon isn’t just about ports. It’s about knowing **what LLM lives behind them**.
