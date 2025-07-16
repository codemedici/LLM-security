# Table of Contents

## Table of contents

* 🏠 About This Notebook

### 📚 Fundamentals

* LLM Security Overview
* LLM Architectures & Deployment Models
* Security Risks in the LLM Lifecycle
* Threat Modeling LLMs
* AI / ML Attack Taxonomy
* Transformer Internals & Security

***

### ⚔️ Threats & Attacks

* **Prompt Injection**
  * Overview
    * Direct
    * Indirect / RAG
    * Multi-Hop & Cross-App
* **Model Influence & Bias**
  * Overview
    * Token Bias & Manipulation
    * Gradient / Embedding Leakage
    * Attention Hijacking & Causal-Mask Exploits
* **Autonomous / Multi-Agent Risks**
  * Autonomous Agent Risks
  * Multi-Agent RCE Chains
* Jailbreaks
* Evasion Attacks & Adversarial Inputs
* Data Extraction & Inference Attacks
* Model Hijacking & Reprogramming
* Prompt Gadget Chains
* Hacking AI Infrastructure Providers

***

### 🧬 Model Manipulation & Supply Chain

* Model Manipulation & Supply-Chain - Overview
  * **Model Backdoors**
    * Overview
      * Custom Layer Injection
      * RLHF Policy Backdoors
      * Pickle / Safetensor Payloads
  * **Supply-Chain Risks**
    * Dataset Poisoning
    * Unsafe Model Loading
    * Lambda-Layer Backdoors

***

### 🛡️ Defensive Engineering

* Defensive Engineering - Overview
* Prompt Isolation & Role Separation
* Output Sanitization & Response Types
* Context-Length Abuse Mitigations
* Ephemeral Memory Control
* Injection-Resistant Agent Design
* RAG Defenses & Retrieval Guardrails
* Embedding Sanitization & Monitoring
* Interpretable Outputs & Trust Calibration
* LLMSecOps Dashboards

***

### 🧪 Evaluation & Hardening

* Evaluation & Hardening - Overview
* Red-Teaming Methodologies
* Adversarial Robustness Evaluation
* Offensive Evaluation Techniques
* Automated Testing Harnesses
* Agent Behavior Trees & Failure Analysis
* Embedding Backdoor Detection
* Hallucination Detection
* RLHF Safety Fine-Tuning
* Reliability Metrics
* Retry Logic & Backoff
  * **Governance, Risk & Compliance**
    * Regulation Overview
    * Transparency & Accountability
    * Watermarking & Provenance
  * **Guardrails & Moderation**
    * Overview
    * Bypass Findings (BH 2024)

***

### 🔍 Monitoring & Detection

* Monitoring & Detection - Overview
* Behavioral Fingerprinting
* Canary Prompts
* Behavior Drift Tracking
* Inference-Time Feature Tracing
* Output Anomaly Detection
* Self-Consistency & Grounding Checks
* LLM-Specific Logging & Observability

***

### ☁️ Runtime Surfaces & Deployment

* Runtime Surfaces - Overview
* LLMSecOps Lifecycle
* Cloud / SaaS Platforms
* Multi-Tenant Isolation Patterns
* Edge AI Threats
* Open-Source API Abuse
* Local Dev & Notebook Risks
* In-Kernel ML Risks

***

### ⛓️ Vector & RAG Security

* Vector & RAG Security - Overview
  * Vector DB Poisoning
  * Embedding Leakage
  * Retrieval-Time Exploits
  * Indirect Prompt Injection (RAG)

***

### ⚙️ Quick-Start Labs

* Lab Index & Setup
  * Prompt Injection Lab
  * Backdoor Model Lab
  * Adversarial RAG Lab
  * Vector Poison Lab
  * Firewall Bypass Lab

***

### 📝 Case Studies & Cheat Sheets

* **Incidents & Vendor Reports**
  * OpenAI System Cards
  * Bug-Bounty Highlights
  * Open-Source Model Compromises
* **Technique Cheat Sheets**
  * Prompt Injection Cheat Sheet
  * RAG Abuse Patterns
  * Adversarial Evaluation Playbook

***

### 📑 Reference Appendices

* Glossary
* Threat Matrix Mapping
* Tooling Index
* Further Reading
