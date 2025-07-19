# Evaluation & Hardening - Overview

## Evaluation & Hardening – Overview

A core component of LLM security is the **systematic evaluation and hardening** of both models and the infrastructure in which they operate. Red teaming, adversarial testing, and behavior auditing are critical not just for identifying model weaknesses, but for closing them through principled defenses.

This section defines what “secure-by-design” and “secure-in-practice” look like for large language models. It distinguishes offensive and defensive evaluation methodologies, and introduces techniques for reinforcing system behavior under adversarial stress.

***

## Why Evaluation Matters

Security in LLMs isn’t static. New jailbreaks, bypasses, and zero-day behaviors emerge regularly — often due to interaction complexity, context length growth, or newly supported modalities (e.g., code execution, tools, image inputs).

Unlike traditional software, LLMs are:

* Probabilistic
* Non-deterministic
* Externally pre-trained

So evaluating and hardening them requires **custom metrics**, tooling, and attack logic.

***

## Evaluation Surfaces

| Surface                    | Focus                                                  |
| -------------------------- | ------------------------------------------------------ |
| **Prompt and input space** | Prompt injections, context poisoning, evasion attacks  |
| **Model internals**        | Backdoors, embedding leakage, alignment drift          |
| **Output space**           | Hallucinations, unsafe completions, misclassification  |
| **Agent behavior**         | Tool misuse, unsafe planning, memory abuse             |
| **Integration layer**      | Retrieval (RAG), plugin chains, multi-agent escalation |

***

## Red Team vs. Hardening Pipeline

| Phase                | Red Team Focus                             | Hardening Focus                       |
| -------------------- | ------------------------------------------ | ------------------------------------- |
| **Discovery**        | Jailbreaks, gadget chains, unsafe defaults | Output sanitization, prompt isolation |
| **Failure analysis** | Unstable completions, RLHF regressions     | Grounding checks, retry logic         |
| **Automation**       | Fuzzing, behavior trees, multi-turn tests  | Rule mining, test harnesses           |
| **GRC compliance**   | Policy violation exposure                  | Regulation-aligned safeguards         |

***

## Key Methods Covered

This section includes:

* Red-Teaming Methodologies
* Adversarial Robustness Evaluation
* Embedding Backdoor Detection
* Behavior Trees and Failure Analysis
* Hallucination Detection
* Retry and Backoff Design
* Safety-Aware Fine-Tuning
* Automated Evaluation Toolchains
* GRC Safeguards and Auditability

***

## Related Pages

* [Defensive Engineering – Overview](https://cosimo.gitbook.io/llm-security/defensive-engineering/overview)
* [Monitoring & Detection](https://cosimo.gitbook.io/llm-security/monitoring-and-detection/overview)
* [Red-Teaming Methodologies](https://cosimo.gitbook.io/llm-security/evaluation-and-hardening/red-teaming-methodologies)

***

## Resources

* OpenAI System Card (GPT-4)
* Anthropic Claude System Card (2023–2024)
* NIST AI RMF 1.0 & AI 100-2e (2025)
* Lakera AI Security Playbook v2
* DEF CON / Black Hat Red Teaming talks (2023–2024)
* Databricks AI Security Framework (DASF)
