# Fine-Tuning & Reinforcement for Safety

## RLHF Safety Fine-Tuning

Reinforcement Learning from Human Feedback (RLHF) is a standard technique for aligning LLM behavior with human preferences and safety constraints. However, improper or insufficient RLHF can lead to exploitable edge cases, biased outputs, or incomplete safety coverage.

This page covers how RLHF interacts with model security, how it can be hardened, and how red teams should evaluate it.

***

## RLHF Security Relevance

RLHF adjusts a model’s preference layer, guiding it to:

* Follow instructions “helpfully” while avoiding unsafe actions
* Reject jailbreaks and policy violations
* Provide calibrated and non-toxic responses

But if adversaries find **blind spots** in this layer, they can:

* Trigger reward hacking or mode collapse
* Reveal RLHF training artifacts
* Force reward-contradicting behavior via clever prompts

***

## Threat Scenarios

| Scenario                      | Attack Vector                                                               |
| ----------------------------- | --------------------------------------------------------------------------- |
| **Reward overfitting**        | Model confidently outputs safe-sounding but hallucinated content            |
| **Policy token memorization** | RLHF filters applied via token-level heuristics that can be bypassed        |
| **Polite jailbreak**          | Adversary uses nice-sounding phrasing to elicit unsafe completions          |
| **Trigger inversion**         | Model rewards prompts that should fail due to prompt collisions or disguise |

***

## Red Teaming RLHF

* Use **differential prompts** (e.g., harsh vs polite jailbreaks)
* Probe model for **instruction leakage** from preference fine-tuning
* Test **edge tone** completions (e.g., satire, sarcasm, hypothetical reasoning)
* Apply **reward inversion** prompts like “What would a harmful model say?”

***

## Fine-Tuning Techniques That Improve Security

| Technique                                 | Description                                                                 |
| ----------------------------------------- | --------------------------------------------------------------------------- |
| **Constitutional AI (Anthropic)**         | Reinforce using model-judged rules rather than human preferences alone      |
| **Policy reward shaping**                 | Apply a strong negative reward to known unsafe completion patterns          |
| **Critic model reranking**                | Use a separate model to re-rank completions based on safety                 |
| **Adversarial rejection sampling**        | Fine-tune model to reject high-risk prompt patterns across diverse phrasing |
| **Uncertainty-aware preference learning** | Reward abstention when the model is unsure or unsupported by context        |

***

## Evaluation Metrics

| Metric                       | Description                                             |
| ---------------------------- | ------------------------------------------------------- |
| **Jailbreak rejection rate** | % of adversarial prompts successfully rejected          |
| **False rejection rate**     | Safe prompts incorrectly rejected                       |
| **Safe completion quality**  | Helpfulness of completions under policy-aligned queries |
| **Policy tone adherence**    | Degree to which the model aligns with stated tone goals |

***

## Related Pages

* [Red-Teaming Methodologies](https://cosimo.gitbook.io/llm-security/evaluation-and-hardening/red-teaming-methodologies)
* [Embedding Backdoor Detection](https://cosimo.gitbook.io/llm-security/evaluation-and-hardening/embedding-space-backdoors)
* [Offensive Evaluation Techniques](https://cosimo.gitbook.io/llm-security/evaluation-and-hardening/offensive-llm-evaluation-techniques)

***

## Resources

* Anthropic Claude System Card (2023–2024) – RLHF and Constitutional AI
* OpenAI Fine-Tuning Guidelines
* Lakera AI Playbook – Preference modeling and reward hacking
* NIST AI 100-2e (2025) – Safety and feedback alignment taxonomies
