# Table of Contents

### Fundamentals

* [Introduction to LLM Security](fundamentals/introduction-to-llm-security.md)
* [LLM Architectures and Deployment Models](fundamentals/llm-architectures-and-deployment-models.md)
* [Transformer Architecture: Security-Critical Internals](fundamentals/transformer-architecture-security-critical-internals.md)
* [Threat Modeling LLMs (STRIDE, MITRE ATLAS, etc.)](fundamentals/threat-modeling-llms.md)
* [AI/ML Attack Taxonomy (NIST AI RMF, AI/ML Threat Matrix)](fundamentals/ai-ml-attack-taxonomy.md)
* [Security Risks in the LLM Lifecycle](fundamentals/security-risks-in-the-llm-lifecycle.md)

### Threats & Attacks

* [Prompt Injection (Direct, Indirect, Multi-Hop)](threats-and-attacks/prompt-injection.md)
* [Jailbreaks (DAN, code, character-level, few-shot exploits)](threats-and-attacks/jailbreaks.md)
* [Data Extraction & Inference Attacks](threats-and-attacks/data-extraction-and-inference-attacks.md)
* [Evasion Attacks & Adversarial Inputs](threats-and-attacks/evasion-attacks-and-adversarial-inputs.md)
* [Model Manipulation: Backdoors, Trojaned Models](broken-reference)
* [Model Hijacking & Reprogramming](threats-and-attacks/model-hijacking-and-reprogramming.md)
* [Causal Mask Exploits and Attention Hijacking](threats-and-attacks/causal-mask-exploits-and-attention-hijacking.md)
* [Autonomous Agent Risks](threats-and-attacks/autonomous-agent-risks.md)

### Model Manipulation

* [Backdoors via Custom Layers and Model Weight Injection](model-manipulation/backdoors-via-custom-layers-and-model-weight-injection.md)

### Evaluation & Hardening

* [Red Teaming Methodologies](evaluation-and-hardening/red-teaming-methodologies.md)
* [Automated Testing of LLMs](evaluation-and-hardening/automated-testing-of-llms.md)
* [Adversarial Robustness Evaluation](evaluation-and-hardening/adversarial-robustness-evaluation.md)
* [Fine-Tuning & Reinforcement for Safety](evaluation-and-hardening/fine-tuning-and-reinforcement-for-safety.md)
* [Guardrails, Moderation APIs, and Filtering](evaluation-and-hardening/guardrails-moderation-apis-and-filtering.md)
* [LLM Hallucination Taxonomy and Detection](evaluation-and-hardening/llm-hallucination-taxonomy-and-detection.md)
* [Reliability Metrics and Evaluation Strategies](evaluation-and-hardening/reliability-metrics-and-evaluation-strategies.md)
* [Retry Logic and Backoff Techniques](evaluation-and-hardening/retry-logic-and-backoff-techniques.md)

### Supply Chain & Serialization Risks

* [Pickle Deserialization and Model Payloads](supply-chain-and-serialization-risks/pickle-deserialization-and-model-payloads.md)
* [Pickle Deserialization and Unsafe Model Loading](supply-chain-and-serialization-risks/pickle-deserialization-and-unsafe-model-loading.md)
* [Custom Layer Injection in Keras/PyTorch](supply-chain-and-serialization-risks/custom-layer-injection-in-keras-pytorch.md)
* [Lambda Layer Backdoors](supply-chain-and-serialization-risks/lambda-layer-backdoors.md)
* [Poisoning Datasets During Pretraining](supply-chain-and-serialization-risks/poisoning-datasets-during-pretraining.md)
* [Dependencies & Model Hosting Supply Chain](supply-chain-and-serialization-risks/dependencies-and-model-hosting-supply-chain.md)

### Platform Surfaces

* [Cloud AI: Azure OpenAI, Sagemaker, GCP](platform-surfaces/cloud-ai-azure-openai-sagemaker-gcp.md)
* [Local Dev: Colab, LambdaLabs, Notebooks](platform-surfaces/local-dev-colab-lambdalabs-notebooks.md)
* [Edge AI Attacks (Mobile, Browser, IoT)](platform-surfaces/edge-ai-attacks.md)
* [Multi-Tenant LLM Deployments](platform-surfaces/multi-tenant-llm-deployments.md)
* [Abuse of Open Source LLM APIs](platform-surfaces/abuse-of-open-source-llm-apis.md)

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

### 🛠️ LLMSecOps Lifecycle

* Dependencies & Model Hosting Supply Chain
* Security Evaluation Checklists
* Custom Harnesses & Evaluation Scripts

### 📦 Vector & RAG Security

* Embedding Space Monitoring
* Retrieval Augmented Generation (RAG) Defenses
* Inference-Time Feature Tracing
* Self-Consistency and Grounding Checks

### 🔐 Governance & Compliance

* Model Card Failures

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
