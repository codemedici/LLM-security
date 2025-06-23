# Table of Contents

### Fundamentals

* Introduction to LLM Security
* LLM Architectures and Deployment Models
* Transformer Architecture: Security-Critical Internals
* Threat Modeling LLMs (STRIDE, MITRE ATLAS, etc.)
* AI/ML Attack Taxonomy (NIST AI RMF, AI/ML Threat Matrix)
* Security Risks in the LLM Lifecycle

### Threats & Attacks

* Prompt Injection (Direct, Indirect, Multi-Hop)
* Jailbreaks (DAN, code, character-level, few-shot exploits)
* Data Extraction & Inference Attacks
* Evasion Attacks & Adversarial Inputs
* Model Manipulation: Backdoors, Trojaned Models
* Model Hijacking & Reprogramming
* Causal Mask Exploits and Attention Hijacking
* Autonomous Agent Risks

### Model Manipulation

* Backdoors via Custom Layers and Model Weight Injection

### Evaluation & Hardening

* Red Teaming Methodologies
* Automated Testing of LLMs
* Adversarial Robustness Evaluation
* Fine-Tuning & Reinforcement for Safety
* Guardrails, Moderation APIs, and Filtering
* LLM Hallucination Taxonomy and Detection
* Reliability Metrics and Evaluation Strategies
* Retry Logic and Backoff Techniques

### Supply Chain & Serialization Risks

* Pickle Deserialization and Model Payloads
* Pickle Deserialization and Unsafe Model Loading
* Custom Layer Injection in Keras/PyTorch
* Lambda Layer Backdoors
* Poisoning Datasets During Pretraining
* Dependencies & Model Hosting Supply Chain

### Platform Surfaces

* Cloud AI: Azure OpenAI, Sagemaker, GCP
* Local Dev: Colab, LambdaLabs, Notebooks
* Edge AI Attacks (Mobile, Browser, IoT)
* Multi-Tenant LLM Deployments
* Abuse of Open Source LLM APIs

### Monitoring & Detection

* LLM-Specific Logging & Observability
* Model Output Anomaly Detection
* Behavioral Fingerprinting
* Canary Prompts
* Inference-Time Feature Tracing
* Continuous Feedback and Behavior Drift
* Self-Consistency and Grounding Checks

### Tools & Techniques

* PyRIT (Microsoft), Garak (HuggingFace), LLMGuard
* Adversarial Robustness Toolbox (ART)
* PromptBench, AdvBench
* LangChain Red Team Modules
* Custom Harnesses & Evaluation Scripts

### Real-World Case Studies

* LLM Incidents & Exploit Walkthroughs
* CTF Challenges (e.g., AI Village, DEF CON)
* Bug Bounty Reports
* Model Card Failures

### Defensive Engineering

* Access Controls & Prompt Isolation
* Output Sanitization & Response Types
* Context Length Abuse Mitigations
* Embedding Space Monitoring
* Retrieval Augmented Generation (RAG) Defenses
* Memory Control and Ephemeral State Isolation
* Interpretable Outputs and Trust Calibration

### Reference Guides

* Common Ports & Services for Recon
* Prompt Wordlists (offensive & defensive)
* LLM-Specific HTTP Headers / APIs
* JSON Schema Fuzzing
* Security Evaluation Checklists
