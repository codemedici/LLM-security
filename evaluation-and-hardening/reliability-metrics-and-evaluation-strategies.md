# Reliability Metrics and Evaluation Strategies

## Reliability Metrics

Evaluating the security of LLMs isn’t only about catching extreme failures — it’s about measuring the model’s **stability**, **consistency**, and **predictability** under both benign and adversarial conditions.

This page introduces key reliability metrics used in LLM security evaluations, including those relevant to red teaming, hallucination detection, alignment drift, and safety regression tracking.

***

## Why Reliability Matters

Unreliable LLMs are:

* Easier to jailbreak
* More prone to hallucinate
* Less robust to prompt fuzzing or adversarial sampling
* Harder to secure through static filtering alone

LLM security demands **measurable trustworthiness** — not just point-in-time compliance.

***

## Core Metric Categories

| Metric                         | Description                                                                     |
| ------------------------------ | ------------------------------------------------------------------------------- |
| **Consistency**                | Degree to which model gives the same output across retries or paraphrases       |
| **Stability under noise**      | Sensitivity to small input changes (typos, whitespace, synonyms)                |
| **Output entropy**             | Variability or randomness of response tokens (esp. in policy-critical segments) |
| **Safety adherence rate**      | % of completions that comply with moderation or alignment goals                 |
| **Behavioral drift**           | Change in output or tone across versions or time windows                        |
| **Rejection precision/recall** | How accurately the model declines unsafe or adversarial inputs                  |

***

## Evaluation Strategies

* **Multi-sampling with fixed prompt**: Run the same prompt 3–10 times and compute agreement score
* **Paraphrase testing**: Reword inputs while preserving semantics; score response similarity
* **Adversarial edge testing**: Slightly exceed known token limits or role boundaries
* **Version regression tracking**: Log changes in output across fine-tuning or RLHF stages
* **Backoff pattern analysis**: Track how and when retry logic engages (e.g., temperature, max tokens)

***

## Common Metrics & Tools

| Metric                            | Tool/Method                                         |
| --------------------------------- | --------------------------------------------------- |
| **BLEU / ROUGE / METEOR**         | Text similarity metrics for paraphrase testing      |
| **JS divergence / KL divergence** | Token distribution divergence for entropy checks    |
| **N-gram diversity**              | Checks for generic or repetitive completions        |
| **Human agreement rate**          | Annotator consensus on safety, correctness, or tone |
| **Prompt fingerprinting**         | Vector-based matching of prompt-output clusters     |

***

## Red Team Applications

* Measure **jailbreak bypass volatility** (e.g., same attack passes 2/5 times)
* Track **alignment drift** as models are updated or retrained
* Identify **output instability hot zones** (e.g., sarcasm, satire, complex queries)
* Compare **policy enforcement consistency** across personas or agents

***

## Related Pages

* [Hallucination Detection](https://cosimo.gitbook.io/llm-security/evaluation-and-hardening/llm-hallucination-taxonomy-and-detection)
* [Retry Logic & Backoff](https://cosimo.gitbook.io/llm-security/evaluation-and-hardening/retry-logic-and-backoff-techniques)
* [Monitoring & Drift Tracking](https://cosimo.gitbook.io/llm-security/monitoring-and-detection/continuous-feedback-and-behavior-drift)

***

## Resources

* Anthropic Claude System Cards (Reliability drift metrics)
* OpenAI GPT-4 Evaluation Report
* NIST AI RMF 1.0 + AI 100-2e: Evaluation criteria for trustworthy AI
* DEF CON 2024 LLM Hallucination and Response Drift Workshop
