# Table of contents

* [Table of Contents](README.md)

## 📖 FUNDAMENTALS

* [LLM Security Overview](fundamentals/llm-security-overview.md)
* [LLM Architectures and Deployment Models](fundamentals/llm-architectures-and-deployment-models.md)
* [Security Risks in the LLM Lifecycle](fundamentals/security-risks-in-the-llm-lifecycle.md)
* [Threat Modeling LLMs](fundamentals/threat-modeling-llms.md)
* [AI/ML Attack Taxonomy](fundamentals/ai-ml-attack-taxonomy.md)
* [Transformer Architecture: Security-Critical Internals](fundamentals/transformer-architecture-security-critical-internals.md)

## ⚔️ Threats & Attacks

* [Prompt Injection](threats-and-attacks/prompt-injection/README.md)
  * [Prompt Injection – Direct](threats-and-attacks/prompt-injection/prompt-injection-direct.md)
  * [Prompt Injection – Indirect / RAG](threats-and-attacks/prompt-injection/prompt-injection-indirect-rag.md)
  * [Prompt Injection – Multi-Hop & Cross-App](threats-and-attacks/prompt-injection/prompt-injection-multi-hop-and-cross-app.md)
  * [Command Injection via Tools & Plugins](threats-and-attacks/prompt-injection/command-injection-via-tools-and-plugins.md)
* [Model Bias](threats-and-attacks/model-bias/README.md)
  * [Token Bias & Manipulation Attacks](threats-and-attacks/model-bias/token-bias-and-manipulation-attacks.md)
  * [Gradient Leakage & Embedding Inversion Attacks](threats-and-attacks/model-bias/gradient-leakage-and-embedding-inversion-attacks.md)
  * [Causal Mask Exploits and Attention Hijacking](threats-and-attacks/model-bias/causal-mask-exploits-and-attention-hijacking.md)
* [Autonomous / Multi-Agent Risks](threats-and-attacks/autonomous-multi-agent-risks/README.md)
  * [Autonomous Agent Risks](threats-and-attacks/autonomous-multi-agent-risks/autonomous-agent-risks.md)
  * [Multi-Agent RCE Chains](threats-and-attacks/autonomous-multi-agent-risks/multi-agent-rce-chains.md)
* [Jailbreaks](threats-and-attacks/jailbreaks.md)
* [Evasion Attacks & Adversarial Inputs](threats-and-attacks/evasion-attacks-and-adversarial-inputs.md)
* [Data Extraction & Inference Attacks](threats-and-attacks/data-extraction-and-inference-attacks.md)
* [Model Hijacking & Reprogramming](threats-and-attacks/model-hijacking-and-reprogramming.md)
* [Prompt Gadget Chains](threats-and-attacks/prompt-gadget-chains.md)
* [Hacking AI Infrastructure Providers](threats-and-attacks/hacking-ai-infrastructure-providers.md)

## 🧬 MODEL MANIPULATION

* [Model Manipulation & Supply Chain](model-manipulation/model-manipulation-and-supply-chain.md)
* [Model Backdoors](model-manipulation/model-backdoors/README.md)
  * [Backdoors via Custom Layers and Model Weight Injection](model-manipulation/model-backdoors/backdoors-via-custom-layers-and-model-weight-injection.md)
  * [RLHF Policy Backdoors](model-manipulation/model-backdoors/rlhf-policy-backdoors.md)
  * [Pickle / Safetensor Payloads](model-manipulation/model-backdoors/pickle-safetensor-payloads.md)
* [Supply-Chain Risks](model-manipulation/supply-chain-risks/README.md)
  * [Dataset Poisoning](model-manipulation/supply-chain-risks/dataset-poisoning.md)
  * [Unsafe Model Loading](model-manipulation/supply-chain-risks/unsafe-model-loading.md)
  * [Lambda-Layer Backdoors](model-manipulation/supply-chain-risks/lambda-layer-backdoors.md)

## 🧱 Defensive Engineering

* [Defensive Engineering - Overview](defensive-engineering/defensive-engineering-overview.md)
* [Access Controls & Prompt Isolation](defensive-engineering/access-controls-and-prompt-isolation.md)
* [Output Sanitization & Response Types](defensive-engineering/output-sanitization-and-response-types.md)
* [Prompt‑Injection‑Resistant Agents](defensive-engineering/prompt-injection-resistant-agents.md)
* [Context Length Abuse Mitigations](defensive-engineering/context-length-abuse-mitigations.md)
* [RAG Defenses & Retrieval Guardrails](defensive-engineering/rag-defenses-and-retrieval-guardrails.md)
* [Embedding Sanitization & Monitoring](defensive-engineering/embedding-sanitization-and-monitoring.md)
* [Ephemeral Memory Control](defensive-engineering/ephemeral-memory-control.md)
* [Interpretable Outputs and Trust Calibration](defensive-engineering/interpretable-outputs-and-trust-calibration.md)
* [LLMSecOps Dashboards](defensive-engineering/llmsecops-dashboards.md)

***

* [Lab 🧪 Secure LLM Agent Design Patterns](lab-secure-llm-agent-design-patterns.md)

## 🛡️ Evaluation & Hardening

* [Evaluation & Hardening - Overview](evaluation-and-hardening/evaluation-and-hardening-overview.md)
* [Red Teaming Methodologies](evaluation-and-hardening/red-teaming-methodologies.md)
* [Adversarial Robustness Evaluation](evaluation-and-hardening/adversarial-robustness-evaluation.md)
* [Offensive LLM Evaluation Techniques](evaluation-and-hardening/offensive-llm-evaluation-techniques.md)
* [Automated Testing of LLMs](evaluation-and-hardening/automated-testing-of-llms.md)
* [Agent Behavior Trees and Failure Analysis](evaluation-and-hardening/agent-behavior-trees-and-failure-analysis.md)
* [Embedding Backdoor Detection](evaluation-and-hardening/embedding-backdoor-detection.md)
* [Hallucination Detection](evaluation-and-hardening/hallucination-detection.md)
* [Fine-Tuning & Reinforcement for Safety](evaluation-and-hardening/fine-tuning-and-reinforcement-for-safety.md)
* [Reliability Metrics and Evaluation Strategies](evaluation-and-hardening/reliability-metrics-and-evaluation-strategies.md)
* [Retry Logic and Backoff](evaluation-and-hardening/retry-logic-and-backoff/README.md)
  * [Governance, Risk & Compliance](evaluation-and-hardening/retry-logic-and-backoff/governance-risk-and-compliance/README.md)
    * [Regulation Overview](evaluation-and-hardening/retry-logic-and-backoff/governance-risk-and-compliance/regulation-overview.md)
    * [Page 6](evaluation-and-hardening/retry-logic-and-backoff/governance-risk-and-compliance/page-6.md)
  * [Guardrails and Moderation](evaluation-and-hardening/retry-logic-and-backoff/guardrails-and-moderation/README.md)
    * [Page 9](evaluation-and-hardening/retry-logic-and-backoff/guardrails-and-moderation/page-9.md)

## 👀 Monitoring & Detection

* [Behavioral Fingerprinting](monitoring-and-detection/behavioral-fingerprinting.md)
* [Canary Prompts](monitoring-and-detection/canary-prompts.md)
* [Continuous Feedback and Behavior Drift](monitoring-and-detection/continuous-feedback-and-behavior-drift.md)
* [LLM Firewall Patterns](monitoring-and-detection/llm-firewall-patterns.md)
* [Model Output Anomaly Detection](monitoring-and-detection/model-output-anomaly-detection.md)
* [Self-Consistency and Grounding Checks](monitoring-and-detection/self-consistency-and-grounding-checks.md)
* [LLM-Specific Logging & Observability](monitoring-and-detection/llm-specific-logging-and-observability.md)

## ☁️ Runtime Surfaces & Deployment

* [Runtime Surfaces - Overview](runtime-surfaces-and-deployment/runtime-surfaces-overview.md)
* [Cloud / SaaS Platforms](runtime-surfaces-and-deployment/cloud-saas-platforms.md)
* [Multi-Tenant Isolation Patterns](runtime-surfaces-and-deployment/multi-tenant-isolation-patterns.md)
* [Edge AI Threats](runtime-surfaces-and-deployment/edge-ai-threats.md)
* [Open-Source API Abuse](runtime-surfaces-and-deployment/open-source-api-abuse.md)
* [Local Dev & Notebook Risks](runtime-surfaces-and-deployment/local-dev-and-notebook-risks.md)

***

* [In-Kernel ML Risks](in-kernel-ml-risks.md)

## 📦 Vector & RAG Security

* [Vector & RAG Security – Overview](vector-and-rag-security/vector-and-rag-security-overview.md)
* [Vector DB Poisoning](vector-and-rag-security/vector-db-poisoning.md)

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

## 📚 Reference Guides

* [Common Ports & Services for Recon](reference-guides/common-ports-and-services-for-recon.md)
* [Prompt Wordlists](reference-guides/prompt-wordlists.md)
* [LLM-Specific HTTP Headers / APIs](reference-guides/llm-specific-http-headers-apis.md)
* [JSON Schema Fuzzing](reference-guides/json-schema-fuzzing.md)

## 🔬 Quick-Start Lab

* [Prompt Injection Lab](quick-start-lab/prompt-injection-lab.md)
* [Pickle Backdoor Lab](quick-start-lab/pickle-backdoor-lab.md)
* [Vector DB Poison Lab](quick-start-lab/vector-db-poison-lab.md)
* [Multi-Hop Agent Prompt Hijacking Lab](quick-start-lab/multi-hop-agent-prompt-hijacking-lab.md)
* [Firewall Bypass Evaluation Lab](quick-start-lab/firewall-bypass-evaluation-lab.md)
