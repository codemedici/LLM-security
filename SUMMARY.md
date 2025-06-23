# Table of contents

* [Project Log](README.md)
* [README](<README (1).md>)
* [Table of Contents](table-of-contents.md)

## 📖 FUNDAMENTALS

* [Introduction to LLM Security](fundamentals/introduction-to-llm-security.md)
* [LLM Architectures and Deployment Models](fundamentals/llm-architectures-and-deployment-models.md)
* [Security Risks in the LLM Lifecycle](fundamentals/security-risks-in-the-llm-lifecycle.md)
* [Threat Modeling LLMs](fundamentals/threat-modeling-llms.md)
* [AI/ML Attack Taxonomy](fundamentals/ai-ml-attack-taxonomy.md)
* [Transformer Architecture: Security-Critical Internals](fundamentals/transformer-architecture-security-critical-internals.md)

## ⚔️ Threats & Attacks

* [Prompt Injection](threats-and-attacks/prompt-injection.md)
* [Autonomous Agent Risks](threats-and-attacks/autonomous-agent-risks.md)
* [Jailbreaks](threats-and-attacks/jailbreaks.md)
* [Data Extraction & Inference Attacks](threats-and-attacks/data-extraction-and-inference-attacks.md)
* [Evasion Attacks & Adversarial Inputs](threats-and-attacks/evasion-attacks-and-adversarial-inputs.md)
* [Model Manipulation: Backdoors, Trojaned Models](threats-and-attacks/model-manipulation-backdoors-trojaned-models.md)
* [Model Hijacking & Reprogramming](threats-and-attacks/model-hijacking-and-reprogramming.md)
* [Causal Mask Exploits and Attention Hijacking](threats-and-attacks/causal-mask-exploits-and-attention-hijacking.md)

## Evaluation & Hardening

* [Red Teaming Methodologies](evaluation-and-hardening/red-teaming-methodologies.md)
* [Agent Behavior Trees and Failure Analysis](evaluation-and-hardening/agent-behavior-trees-and-failure-analysis.md)
* [Automated Testing of LLMs](evaluation-and-hardening/automated-testing-of-llms.md)
* [Adversarial Robustness Evaluation](evaluation-and-hardening/adversarial-robustness-evaluation.md)
* [Fine-Tuning & Reinforcement for Safety](evaluation-and-hardening/fine-tuning-and-reinforcement-for-safety.md)
* [Guardrails, Moderation APIs, and Filtering](evaluation-and-hardening/guardrails-moderation-apis-and-filtering.md)
* [LLM Hallucination Taxonomy and Detection](evaluation-and-hardening/llm-hallucination-taxonomy-and-detection.md)
* [Reliability Metrics and Evaluation Strategies](evaluation-and-hardening/reliability-metrics-and-evaluation-strategies.md)
* [Retry Logic and Backoff Techniques](evaluation-and-hardening/retry-logic-and-backoff-techniques.md)

## Supply Chain & Serialization Risks

* [Pickle Deserialization & Model Payloads](supply-chain-and-serialization-risks/pickle-deserialization-and-model-payloads.md)
* [Custom Layer Injection in Keras/PyTorch](supply-chain-and-serialization-risks/custom-layer-injection-in-keras-pytorch.md)
* [Lambda Layer Backdoors](supply-chain-and-serialization-risks/lambda-layer-backdoors.md)
* [Poisoning Datasets During Pretraining](supply-chain-and-serialization-risks/poisoning-datasets-during-pretraining.md)
* [Pickle Deserialization and Unsafe Model Loading](supply-chain-and-serialization-risks/pickle-deserialization-and-unsafe-model-loading.md)

## Platform Surfaces

* [Cloud AI: Azure OpenAI, Sagemaker, GCP](platform-surfaces/cloud-ai-azure-openai-sagemaker-gcp.md)
* [Local Dev: Colab, LambdaLabs, Notebooks](platform-surfaces/local-dev-colab-lambdalabs-notebooks.md)
* [Edge AI Attacks](platform-surfaces/edge-ai-attacks.md)
* [Multi-Tenant LLM Deployments](platform-surfaces/multi-tenant-llm-deployments.md)
* [Abuse of Open Source LLM APIs](platform-surfaces/abuse-of-open-source-llm-apis.md)

## Monitoring & Detection

* [LLM-Specific Logging & Observability](monitoring-and-detection/llm-specific-logging-and-observability.md)
* [Model Output Anomaly Detection](monitoring-and-detection/model-output-anomaly-detection.md)
* [Behavioral Fingerprinting](monitoring-and-detection/behavioral-fingerprinting.md)
* [Canary Prompts](monitoring-and-detection/canary-prompts.md)
* [Continuous Feedback and Behavior Drift](monitoring-and-detection/continuous-feedback-and-behavior-drift.md)
* [Self-Consistency and Grounding Checks](monitoring-and-detection/self-consistency-and-grounding-checks.md)

## Tools & Techniques

* [PyRIT, Garak, LLMGuard](tools-and-techniques/pyrit-garak-llmguard.md)
* [Adversarial Robustness Toolbox (ART)](tools-and-techniques/adversarial-robustness-toolbox-art.md)
* [PromptBench, AdvBench](tools-and-techniques/promptbench-advbench.md)
* [LangChain Red Team Modules](tools-and-techniques/langchain-red-team-modules.md)
* [CrewAI & AutoGen Security Models](tools-and-techniques/crewai-and-autogen-security-models.md)

## Real-World Case Studies

***

* [LLM Incidents & Exploit Walkthroughs](llm-incidents-and-exploit-walkthroughs.md)
* [CTF Challenges](ctf-challenges/README.md)
  * [Hack The Box](ctf-challenges/hack-the-box/README.md)
    * [AI SPACE](ctf-challenges/hack-the-box/ai-space.md)
* [Bug Bounty Reports](bug-bounty-reports.md)

## Defensive Engineering

* [Access Controls & Prompt Isolation](defensive-engineering/access-controls-and-prompt-isolation.md)
* [Memory Control and Ephemeral State Isolation](defensive-engineering/memory-control-and-ephemeral-state-isolation.md)
* [Output Sanitization & Response Types](defensive-engineering/output-sanitization-and-response-types.md)
* [Context Length Abuse Mitigations](defensive-engineering/context-length-abuse-mitigations.md)
* [Interpretable Outputs and Trust Calibration](defensive-engineering/interpretable-outputs-and-trust-calibration.md)

## Reference Guides

* [Common Ports & Services for Recon](reference-guides/common-ports-and-services-for-recon.md)
* [Prompt Wordlists](reference-guides/prompt-wordlists.md)
* [LLM-Specific HTTP Headers / APIs](reference-guides/llm-specific-http-headers-apis.md)
* [JSON Schema Fuzzing](reference-guides/json-schema-fuzzing.md)

## MODEL MANIPULATION

* [Backdoors via Custom Layers and Model Weight Injection](model-manipulation/backdoors-via-custom-layers-and-model-weight-injection.md)

## 🔐 Governance & Compliance

* [Model Card Failures](governance-and-compliance/model-card-failures.md)

## 🛠️ LLMSecOps Lifecycle

* [Dependencies & Model Hosting Supply Chain](llmsecops-lifecycle/dependencies-and-model-hosting-supply-chain.md)
* [Security Evaluation Checklists](llmsecops-lifecycle/security-evaluation-checklists.md)
* [Custom Harnesses & Evaluation Scripts](llmsecops-lifecycle/custom-harnesses-and-evaluation-scripts.md)

## 📦 Vector & RAG Security

* [Embedding Space Monitoring](vector-and-rag-security/embedding-space-monitoring.md)
* [Inference-Time Feature Tracing](vector-and-rag-security/inference-time-feature-tracing.md)
* [Retrieval Augmented Generation (RAG) Defenses](vector-and-rag-security/retrieval-augmented-generation-rag-defenses.md)
* [Self-Consistency and Grounding Checks](vector-and-rag-security/self-consistency-and-grounding-checks.md)
