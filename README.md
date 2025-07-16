# Table of Contents

## Table of contents

* Table of Contents

### 📖 Fundamentals

* Introduction to LLM Security
* LLM Architectures and Deployment Models
* Security Risks in the LLM Lifecycle
* Threat Modeling LLMs
* AI/ML Attack Taxonomy
* Transformer Architecture: Security-Critical Internals

### ⚔️ Threats & Attacks

* Prompt Injection – Direct
* Prompt Injection – Indirect / RAG
* Prompt Injection – Multi-Hop & Cross-App
* Autonomous Agent Risks
* Jailbreaks
* Evasion Attacks & Adversarial Inputs
* Data Extraction & Inference Attacks
* Gradient Leakage & Embedding Inversion Attacks
* Causal Mask Exploits and Attention Hijacking
* Prompt Gadget Chains
* Token Bias & Manipulation Attacks
* Multi-Agent RCE Chains
* Model Hijacking & Reprogramming
* Model Manipulation: Backdoors & Trojaned Models
* Hacking AI Infrastructure Providers

### 🧬 Model Manipulation & Supply Chain

* Backdoors via Custom Layers and Weight Injection
* Pickle Deserialization & Model Payloads
* Unsafe Model Loading
* Custom Layer Injection in Keras/PyTorch
* Lambda Layer Backdoors
* Poisoning Datasets During Pretraining
* RLHF Policy Weight Backdoors

### 🛡️ Defensive Engineering

* Prompt Isolation & Role Separation
* Output Sanitization and Response Types
* Context Length Abuse Mitigations
* Memory Control and Ephemeral State Isolation
* Design Patterns for Prompt Injection-Resistant Agents
* RAG Defenses
* Embedding Sanitization & Monitoring
* Interpretable Outputs and Trust Calibration
* LLMSecOps Dashboards

### 🧪 Evaluation & Hardening

* Red Teaming Methodologies
* Adversarial Robustness Evaluation
* Offensive LLM Evaluation Techniques
* Automated Testing of LLMs
* Agent Behavior Trees and Failure Analysis
* Embedding Space Backdoors
* LLM Hallucination Taxonomy and Detection
* Fine-Tuning and Reinforcement for Safety
* Reliability Metrics and Evaluation Strategies
* Retry Logic and Backoff Techniques
* Guardrails, Moderation APIs, and Filtering
  * Bypass Findings from Black Hat 2024

### 🔍 Monitoring & Detection

* Behavioral Fingerprinting
* Canary Prompts
* Continuous Feedback and Behavior Drift
* Inference-Time Feature Tracing
* Model Output Anomaly Detection
* Self-Consistency and Grounding Checks
* LLM-Specific Logging and Observability

### 🔁 LLMsecOps Lifecycle

* LLMSecOps Lifecycle
* MLOps to MLooPS: Exposed Attack Surfaces

### 🌐 Platform Surfaces

* Cloud AI: Azure, OpenAI, Sagemaker, GCP
* Multi-Tenant LLM Deployments
* Edge AI Attacks
* Abuse of Open Source LLM APIs
* Local Dev: Colab, Lambda, Notebooks
* In-Kernel ML Security Risks

### ⛓️ Vector & RAG Security

* Vector DB Poisoning
* Embedding Leakage and Vector Exposure
* Inference-Time Retrieval Exploits

### 📜 Governance & Compliance

* Regulation Overview
* Transparency and Accountability in Red Teaming
* Watermarking and Provenance in LLM Outputs

### 🧪 Quick-Start Labs

* Prompt Injection Lab
* Pickle Backdoor Lab
* Vector DB Poison Lab
* Multi-Hop Agent Prompt Hijacking Lab
* Firewall Bypass Evaluation Lab

### 📚 Reference Guides

* Prompt Wordlists
* Common Ports and Services for Recon
* LLM-Specific HTTP Headers & APIs
* JSON Schema Fuzzing
* Security Evaluation Checklists

### 📁 Case Studies

* LLM Agent Security Case Studies
* OpenAI’s External Red Teaming Approach
* Bug Bounty Reports
* LLM Incidents and Exploit Walkthroughs
* Pattern Mapping Cheat Sheet
* Practical LLM Security Takeaways
