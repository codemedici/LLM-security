# Table of contents

* [Table of Contents](README.md)

## 🔬 Quick-Start Lab

* [Prompt Injection Lab](quick-start-lab/prompt-injection-lab.md)
* [Pickle Backdoor Lab](quick-start-lab/pickle-backdoor-lab.md)
* [Vector DB Poison Lab](quick-start-lab/vector-db-poison-lab.md)
* [Multi-Hop Agent Prompt Hijacking Lab](quick-start-lab/multi-hop-agent-prompt-hijacking-lab.md)
* [Firewall Bypass Evaluation Lab](quick-start-lab/firewall-bypass-evaluation-lab.md)

## 📖 FUNDAMENTALS

* [Introduction to LLM Security](fundamentals/introduction-to-llm-security.md)
* [LLM Architectures and Deployment Models](fundamentals/llm-architectures-and-deployment-models.md)
* [Security Risks in the LLM Lifecycle](fundamentals/security-risks-in-the-llm-lifecycle.md)
* [Threat Modeling LLMs](fundamentals/threat-modeling-llms.md)
* [AI/ML Attack Taxonomy](fundamentals/ai-ml-attack-taxonomy.md)
* [Transformer Architecture: Security-Critical Internals](fundamentals/transformer-architecture-security-critical-internals.md)

## ⚔️ Threats & Attacks

* [Prompt Injection – Direct](threats-and-attacks/prompt-injection-direct.md)
* [Prompt Injection – Indirect / RAG](threats-and-attacks/prompt-injection-indirect-rag.md)
* [Prompt Injection – Multi-Hop & Cross-App](threats-and-attacks/prompt-injection-multi-hop-and-cross-app.md)
* [Autonomous Agent Risks](threats-and-attacks/autonomous-agent-risks.md)
* [Jailbreaks](threats-and-attacks/jailbreaks.md)
* [Data Extraction & Inference Attacks](threats-and-attacks/data-extraction-and-inference-attacks.md)
* [Evasion Attacks & Adversarial Inputs](threats-and-attacks/evasion-attacks-and-adversarial-inputs.md)
* [Model Manipulation: Backdoors, Trojaned Models](threats-and-attacks/model-manipulation-backdoors-trojaned-models.md)
* [Model Hijacking & Reprogramming](threats-and-attacks/model-hijacking-and-reprogramming.md)
* [Causal Mask Exploits and Attention Hijacking](threats-and-attacks/causal-mask-exploits-and-attention-hijacking.md)
* [Hacking AI Infrastructure Providers](threats-and-attacks/hacking-ai-infrastructure-providers.md)
* [Prompt Gadget Chains](threats-and-attacks/prompt-gadget-chains.md)
* [Token Bias & Manipulation Attacks](threats-and-attacks/token-bias-and-manipulation-attacks.md)
* [Multi-Agent RCE Chains](threats-and-attacks/multi-agent-rce-chains.md)
* [Gradient Leakage & Embedding Inversion Attacks](threats-and-attacks/gradient-leakage-and-embedding-inversion-attacks.md)

## 🧬 MODEL MANIPULATION

* [Backdoors via Custom Layers and Model Weight Injection](model-manipulation/backdoors-via-custom-layers-and-model-weight-injection.md)

## 🛡️ Evaluation & Hardening

* [Red Teaming Methodologies](evaluation-and-hardening/red-teaming-methodologies.md)
* [Agent Behavior Trees and Failure Analysis](evaluation-and-hardening/agent-behavior-trees-and-failure-analysis.md)
* [Automated Testing of LLMs](evaluation-and-hardening/automated-testing-of-llms.md)
* [Adversarial Robustness Evaluation](evaluation-and-hardening/adversarial-robustness-evaluation.md)
* [Fine-Tuning & Reinforcement for Safety](evaluation-and-hardening/fine-tuning-and-reinforcement-for-safety.md)
* [Guardrails, Moderation APIs, and Filtering](evaluation-and-hardening/guardrails-moderation-apis-and-filtering/README.md)
  * [Bypass Findings from Black Hat 2024](evaluation-and-hardening/guardrails-moderation-apis-and-filtering/bypass-findings-from-black-hat-2024.md)
* [LLM Hallucination Taxonomy and Detection](evaluation-and-hardening/llm-hallucination-taxonomy-and-detection.md)
* [Reliability Metrics and Evaluation Strategies](evaluation-and-hardening/reliability-metrics-and-evaluation-strategies.md)
* [Retry Logic and Backoff Techniques](evaluation-and-hardening/retry-logic-and-backoff-techniques.md)
* [Offensive LLM Evaluation Techniques](evaluation-and-hardening/offensive-llm-evaluation-techniques.md)
* [Embedding Space Backdoors](evaluation-and-hardening/embedding-space-backdoors.md)
* [Secure Design Patterns for LLM Agents](evaluation-and-hardening/secure-design-patterns-for-llm-agents.md)
* [Secure Design Patterns for LLM Agents](evaluation-and-hardening/secure-design-patterns-for-llm-agents-1.md)

## ⛓️ Supply Chain & Serialization Risks

* [Pickle Deserialization & Model Payloads](supply-chain-and-serialization-risks/pickle-deserialization-and-model-payloads.md)
* [Custom Layer Injection in Keras/PyTorch](supply-chain-and-serialization-risks/custom-layer-injection-in-keras-pytorch.md)
* [Lambda Layer Backdoors](supply-chain-and-serialization-risks/lambda-layer-backdoors.md)
* [Poisoning Datasets During Pretraining](supply-chain-and-serialization-risks/poisoning-datasets-during-pretraining.md)
* [Pickle Deserialization and Unsafe Model Loading](supply-chain-and-serialization-risks/pickle-deserialization-and-unsafe-model-loading.md)
* [RLHF Policy Weight Backdoors](supply-chain-and-serialization-risks/rlhf-policy-weight-backdoors.md)

## 🌐 Platform Surfaces

* [Cloud AI: Azure OpenAI, Sagemaker, GCP](platform-surfaces/cloud-ai-azure-openai-sagemaker-gcp.md)
* [Local Dev: Colab, LambdaLabs, Notebooks](platform-surfaces/local-dev-colab-lambdalabs-notebooks.md)
* [Edge AI Attacks](platform-surfaces/edge-ai-attacks.md)
* [Multi-Tenant LLM Deployments](platform-surfaces/multi-tenant-llm-deployments.md)
* [Abuse of Open Source LLM APIs](platform-surfaces/abuse-of-open-source-llm-apis.md)
* [In-Kernel ML Security Risks](platform-surfaces/in-kernel-ml-security-risks.md)
* [LLM Abuse via Edge Devices & IoT](platform-surfaces/llm-abuse-via-edge-devices-and-iot.md)

## 👀 Monitoring & Detection

* [LLM-Specific Logging & Observability](monitoring-and-detection/llm-specific-logging-and-observability.md)
* [Model Output Anomaly Detection](monitoring-and-detection/model-output-anomaly-detection.md)
* [Behavioral Fingerprinting](monitoring-and-detection/behavioral-fingerprinting.md)
* [Canary Prompts](monitoring-and-detection/canary-prompts.md)
* [Continuous Feedback and Behavior Drift](monitoring-and-detection/continuous-feedback-and-behavior-drift.md)
* [Self-Consistency and Grounding Checks](monitoring-and-detection/self-consistency-and-grounding-checks.md)
* [LLM Firewall Patterns](monitoring-and-detection/llm-firewall-patterns.md)

## 🧰 Tools & Techniques

* [PyRIT, Garak, LLMGuard](tools-and-techniques/pyrit-garak-llmguard.md)
* [Adversarial Robustness Toolbox (ART)](tools-and-techniques/adversarial-robustness-toolbox-art.md)
* [PromptBench, AdvBench](tools-and-techniques/promptbench-advbench.md)
* [LangChain Red Team Modules](tools-and-techniques/langchain-red-team-modules.md)
* [CrewAI & AutoGen Security Models](tools-and-techniques/crewai-and-autogen-security-models.md)
* [Lakera & Prompt Shield Quick-Start](tools-and-techniques/lakera-and-prompt-shield-quick-start.md)

## 🔄 LLMSecOps Lifecycle

* [Dependencies & Model Hosting Supply Chain](supply-chain-and-serialization-risks/dependencies-and-model-hosting-supply-chain.md)
* [Security Evaluation Checklists](reference-guides/security-evaluation-checklists.md)
* [Custom Harnesses & Evaluation Scripts](tools-and-techniques/custom-harnesses-and-evaluation-scripts.md)
* [MLOps to MLOops: Exposed Attack Surface](llmsecops-lifecycle/mlops-to-mloops-exposed-attack-surface.md)
* [LLMSecOps Lifecycle](llmsecops-lifecycle/llmsecops-lifecycle.md)

## 📦 Vector & RAG Security

* [Embedding Space Monitoring](defensive-engineering/embedding-space-monitoring.md)
* [Inference-Time Feature Tracing](monitoring-and-detection/inference-time-feature-tracing.md)
* [Retrieval Augmented Generation (RAG) Defenses](defensive-engineering/retrieval-augmented-generation-rag-defenses.md)
* [Self-Consistency and Grounding Checks](vector-and-rag-security/self-consistency-and-grounding-checks.md)
* [Retrieval Poisoning & Filtering Strategies](vector-and-rag-security/retrieval-poisoning-and-filtering-strategies.md)
* [Weaviate & pgvector Hardening Checklist](vector-and-rag-security/weaviate-and-pgvector-hardening-checklist.md)

## 🔐 Governance & Compliance

* [Model Card Failures](model-card-failures.md)
* [Regulation Overview](governance-and-compliance/regulation-overview.md)
* [Watermarking & Provenance in LLM Outputs](governance-and-compliance/watermarking-and-provenance-in-llm-outputs.md)
* [Transparency & Accountability in Red Teaming](governance-and-compliance/transparency-and-accountability-in-red-teaming.md)

## 📝 Case Studies

* [LLM Incidents & Exploit Walkthroughs](case-studies/llm-incidents-and-exploit-walkthroughs.md)
* [Practical LLM Security Takeaways](case-studies/practical-llm-security-takeaways.md)
* [Pattern Mapping Cheat‑Sheet](case-studies/pattern-mapping-cheat-sheet.md)
* [CTF Challenges](case-studies/ctf-challenges/README.md)
  * [Hack The Box](case-studies/ctf-challenges/hack-the-box/README.md)
    * [AI SPACE](case-studies/ctf-challenges/hack-the-box/ai-space.md)
* [Bug Bounty Reports](case-studies/bug-bounty-reports.md)
* [LLM Agent Security Case Studies](case-studies/llm-agent-security-case-studies.md)
* [OpenAI's Approach to External Red Teaming for AI Models and Systems](case-studies/openais-approach-to-external-red-teaming-for-ai-models-and-systems.md)

## 🧱 Defensive Engineering

* [Access Controls & Prompt Isolation](defensive-engineering/access-controls-and-prompt-isolation.md)
* [Memory Control and Ephemeral State Isolation](defensive-engineering/memory-control-and-ephemeral-state-isolation.md)
* [Output Sanitization & Response Types](defensive-engineering/output-sanitization-and-response-types.md)
* [Context Length Abuse Mitigations](defensive-engineering/context-length-abuse-mitigations.md)
* [Interpretable Outputs and Trust Calibration](defensive-engineering/interpretable-outputs-and-trust-calibration.md)
* [LLMSecOps Pipeline & Dashboards](defensive-engineering/llmsecops-pipeline-and-dashboards.md)
* [Design Patterns for Prompt‑Injection‑Resistant Agents](defensive-engineering/design-patterns-for-prompt-injection-resistant-agents.md)

## 📚 Reference Guides

* [Common Ports & Services for Recon](reference-guides/common-ports-and-services-for-recon.md)
* [Prompt Wordlists](reference-guides/prompt-wordlists.md)
* [LLM-Specific HTTP Headers / APIs](reference-guides/llm-specific-http-headers-apis.md)
* [JSON Schema Fuzzing](reference-guides/json-schema-fuzzing.md)
