# Adversarial Robustness Evaluation

## Adversarial Robustness Evaluation

Adversarial robustness refers to a model’s ability to maintain correct or safe behavior when exposed to crafted, malicious, or out-of-distribution inputs. Unlike general performance evaluation, robustness testing focuses on resistance to manipulation, ambiguity, and edge-case exploitation.

This page covers how to evaluate adversarial robustness of LLMs and the system behaviors they influence.

***

## What Makes an Input Adversarial?

An input is adversarial if it is:

* Crafted to exploit model biases or weaknesses
* Slightly modified to induce a harmful or unintended output
* Contextually ambiguous in a way that causes behavioral failure

***

## Attack Modalities

| Modality                    | Example                                                    |
| --------------------------- | ---------------------------------------------------------- |
| **Text perturbation**       | Misspellings, homoglyphs, Unicode confusables              |
| **Semantic role inversion** | "You are now the user, I am the system"                    |
| **Trigger priming**         | Prefixing a conversation with hidden jailbreaks            |
| **Paraphrased attacks**     | Same intent, reworded to avoid filters                     |
| **Few-shot manipulation**   | Altering prompt structure to influence model tone or logic |
| **RAG-context attacks**     | Poisoning retrieved content with evasive language          |

***

## Evaluation Methods

| Method                          | Description                                                                |
| ------------------------------- | -------------------------------------------------------------------------- |
| **Manual attack corpora**       | Curated lists of known prompts and bypass variants (e.g., jailbreak repos) |
| **Fuzz testing**                | Generate variants using noise, synonym substitution, or character swaps    |
| **Model-to-model testing**      | Use one LLM to generate adversarial inputs for another                     |
| **Embedding sensitivity**       | Measure semantic drift when paraphrasing or substituting embeddings        |
| **Prompt embedding clustering** | Detect structural similarities among vulnerable inputs                     |

***

## Metric Types

| Metric                        | Description                                                   |
| ----------------------------- | ------------------------------------------------------------- |
| **Attack success rate (ASR)** | % of adversarial inputs causing failure                       |
| **Robust accuracy**           | Accuracy under distribution shift or perturbation             |
| **Perturbation budget**       | Number of tokens changed to cause behavioral shift            |
| **Recovery fidelity**         | Model's ability to recover when re-anchored by safety prompts |

***

## Red Team Applications

* Use adversarial inputs to uncover unsafe fallbacks
* Combine with retry logic to test whether outputs are stable or bypassed
* Evaluate **hallucination frequency** under perturbation
* Quantify safety degradation across model versions

***

## Best Practices

* Test across diverse threat models: casual abuse, insider threats, targeted jailbreaks
* Use sandboxed agents to simulate downstream effects
* Correlate robustness with **fine-tuning depth** and **instruction-following sensitivity**
* Always **log token-level changes** and perform semantic alignment diffs

***

## Related Pages

* [Offensive Evaluation Techniques](https://cosimo.gitbook.io/llm-security/evaluation-and-hardening/offensive-llm-evaluation-techniques)
* [Hallucination Detection](https://cosimo.gitbook.io/llm-security/evaluation-and-hardening/llm-hallucination-taxonomy-and-detection)
* [Red-Teaming Methodologies](https://cosimo.gitbook.io/llm-security/evaluation-and-hardening/red-teaming-methodologies)

***

## Resources

* “Universal and Transferable Adversarial Attacks on Aligned Language Models” – Zou et al. (2023)
* OpenAI Red Teaming Notes on adversarial inputs (2023)
* Anthropic Claude alignment and jailbreaking evaluation (System Cards)
* Lakera AI Prompt Injection Handbook v2
