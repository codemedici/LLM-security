# Table of contents

* [README](README.md)
* [Table of Contents](table-of-contents.md)

## 📂 FUNDAMENTALS

* [Introduction to LLM Security](fundamentals/introduction-to-llm-security.md)
* [LLM Architectures and Deployment Models](fundamentals/llm-architectures-and-deployment-models.md)

***

* [Threat Modeling LLMs](threat-modeling-llms.md)
* [AI/ML Attack Taxonomy](ai-ml-attack-taxonomy.md)
* [Security Risks in the LLM Lifecycle](security-risks-in-the-llm-lifecycle.md)

## Threats & Attacks

* [Prompt Injection (Direct, Indirect, Multi-Hop)](threats-and-attacks/prompt-injection-direct-indirect-multi-hop.md)

***

* [Jailbreaks (DAN, code, character-level, few-shot exploits)](jailbreaks-dan-code-character-level-few-shot-exploits.md)
* [Data Extraction & Inference Attacks](data-extraction-and-inference-attacks.md)
* [Evasion Attacks & Adversarial Inputs](evasion-attacks-and-adversarial-inputs.md)
* [Model Manipulation: Backdoors, Trojaned Models](model-manipulation-backdoors-trojaned-models.md)
* [Model Hijacking & Reprogramming](model-hijacking-and-reprogramming.md)

## Evaluation & Hardening

* [Red Teaming Methodologies](evaluation-and-hardening/red-teaming-methodologies.md)

***

* [Automated Testing of LLMs](automated-testing-of-llms.md)
* [Adversarial Robustness Evaluation](adversarial-robustness-evaluation.md)
* [Fine-Tuning & Reinforcement for Safety](fine-tuning-and-reinforcement-for-safety.md)
* [Guardrails, Moderation APIs, and Filtering](guardrails-moderation-apis-and-filtering.md)

## Supply Chain & Serialization Risks

* [Pickle Deserialization & Model Payloads](supply-chain-and-serialization-risks/pickle-deserialization-and-model-payloads.md)
* [Custom Layer Injection in Keras/PyTorch](supply-chain-and-serialization-risks/custom-layer-injection-in-keras-pytorch.md)

***

* [Lambda Layer Backdoors](lambda-layer-backdoors.md)
* [Poisoning Datasets During Pretraining](poisoning-datasets-during-pretraining.md)
* [Dependencies & Model Hosting Supply Chain](dependencies-and-model-hosting-supply-chain.md)

## Platform Surfaces

* [Cloud AI: Azure OpenAI, Sagemaker, GCP](platform-surfaces/cloud-ai-azure-openai-sagemaker-gcp.md)
* [Local Dev: Colab, LambdaLabs, Notebooks](platform-surfaces/local-dev-colab-lambdalabs-notebooks.md)
* [Edge AI Attacks (Mobile, Browser, IoT)](platform-surfaces/edge-ai-attacks-mobile-browser-iot.md)
* [Multi-Tenant LLM Deployments](platform-surfaces/multi-tenant-llm-deployments.md)
* [Abuse of Open Source LLM APIs](platform-surfaces/abuse-of-open-source-llm-apis.md)

## Monitoring & Detection

* [LLM-Specific Logging & Observability](monitoring-and-detection/llm-specific-logging-and-observability.md)
* [Model Output Anomaly Detection](monitoring-and-detection/model-output-anomaly-detection.md)
* [Behavioral Fingerprinting](monitoring-and-detection/behavioral-fingerprinting.md)
* [Canary Prompts](monitoring-and-detection/canary-prompts.md)
* [Inference-Time Feature Tracing](monitoring-and-detection/inference-time-feature-tracing.md)

## Tools & Techniques

* [PyRIT, Garak, LLMGuard](tools-and-techniques/pyrit-garak-llmguard.md)
* [Adversarial Robustness Toolbox (ART)](tools-and-techniques/adversarial-robustness-toolbox-art.md)
* [PromptBench, AdvBench](tools-and-techniques/promptbench-advbench.md)
* [LangChain Red Team Modules](tools-and-techniques/langchain-red-team-modules.md)
* [Custom Harnesses & Evaluation Scripts](tools-and-techniques/custom-harnesses-and-evaluation-scripts.md)

## Real-World Case Studies

***

* [LLM Incidents & Exploit Walkthroughs](llm-incidents-and-exploit-walkthroughs.md)
* [CTF Challenges](ctf-challenges.md)
* [Bug Bounty Reports](bug-bounty-reports.md)
* [Model Card Failures](model-card-failures.md)

## Defensive Engineering

* [Access Controls & Prompt Isolation](defensive-engineering/access-controls-and-prompt-isolation.md)

***

* [Output Sanitization & Response Types](output-sanitization-and-response-types.md)
* [Context Length Abuse Mitigations](context-length-abuse-mitigations.md)
* [Embedding Space Monitoring](embedding-space-monitoring.md)
* [Retrieval Augmented Generation (RAG) Defenses](retrieval-augmented-generation-rag-defenses.md)

## Reference Guides

* [Common Ports & Services for Recon](reference-guides/common-ports-and-services-for-recon.md)
* [Prompt Wordlists (offensive & defensive)](reference-guides/prompt-wordlists-offensive-and-defensive.md)
* [LLM-Specific HTTP Headers / APIs](reference-guides/llm-specific-http-headers-apis.md)
* [JSON Schema Fuzzing](reference-guides/json-schema-fuzzing.md)
* [Security Evaluation Checklists](reference-guides/security-evaluation-checklists.md)

## 📔 Personal

* [Hack The Box](personal/hack-the-box/README.md)
  * [AI SPACE](personal/hack-the-box/ai-space.md)
