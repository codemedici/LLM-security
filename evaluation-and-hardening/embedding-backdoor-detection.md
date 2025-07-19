# Embedding Backdoor Detection

## Embedding Backdoor Detection

Backdoors can be hidden in model weights, activations, or embedding spaces — triggered only by specific inputs that resemble normal user prompts. These embedding-level triggers are particularly stealthy: they may not alter visible behavior until precisely activated.

This page explains how to detect embedding backdoors in LLMs, particularly in open-source and fine-tuned models.

***

## What Is an Embedding Backdoor?

An embedding backdoor is a latent vulnerability introduced during training or fine-tuning that causes the model to:

* Behave differently when exposed to specific token sequences or embeddings
* Bypass safety mechanisms or switch into a hidden mode
* Leak information or reveal alternate functionality

These can be injected via:

* Pretraining dataset poisoning
* Activation-level fine-tuning
* Embedding space perturbation
* Alignment-time adversarial triggers

***

## Real-World Risk Scenarios

| Scenario                          | Impact                                                                                  |
| --------------------------------- | --------------------------------------------------------------------------------------- |
| **Trigger word causes jailbreak** | A single obscure phrase (e.g., `"*unlockmode"`), when embedded, disables safety filters |
| **Custom activation path**        | Input embeds that map to a hidden function selector                                     |
| **Leaked latent code**            | Embedding matches secret memory that unlocks backdoor behavior                          |
| **Multilingual backdoor**         | Triggers only present in low-resource language tokens or special symbols                |

***

## Detection Techniques

| Method                           | Description                                                                                |
| -------------------------------- | ------------------------------------------------------------------------------------------ |
| **Trigger activation scanning**  | Feed controlled inputs and measure anomalous neuron or attention activations               |
| **Embedding outlier detection**  | Cluster embeddings; outliers may encode injected triggers                                  |
| **Reverse influence functions**  | Map outputs back to training examples that may have poisoned activations                   |
| **Subspace projection analysis** | Check for overrepresented directions in latent space that correlate with behavioral change |
| **Manual canary triggering**     | Use known trigger formats (typos, hex, ROT13, homoglyphs) to elicit response changes       |

***

## Red Team Process

1. Load model in sandboxed eval harness
2. Query with known benign and semi-random inputs
3. Log output distribution and attention activation
4. Look for latent behavior toggles or dramatic output shifts
5. Repeat with input embedding perturbations

***

## Defensive Measures

| Strategy                        | Benefit                                              |
| ------------------------------- | ---------------------------------------------------- |
| **Embed space regularization**  | Prevent sharp decision boundaries in latent space    |
| **Backdoor fine-tuning scans**  | Use dedicated prompts to test for latent triggers    |
| **Embedding norm constraints**  | Limit impact of outlier embeddings                   |
| **Activation pattern auditing** | Instrument model to detect abnormal neuron spikes    |
| **Diversity-based retraining**  | Dilute any poisoned subspace via wide input exposure |

***

## Related Pages

* [Model Backdoors – Overview](https://cosimo.gitbook.io/llm-security/model-manipulation/model-backdoors/overview)
* [Custom Layer Injection](https://cosimo.gitbook.io/llm-security/model-manipulation/model-backdoors/custom-layer-injection)
* [Red-Teaming Methodologies](https://cosimo.gitbook.io/llm-security/evaluation-and-hardening/red-teaming-methodologies)

***

## Resources

* “Hidden Trigger Backdoors in NLP Models” (Zhou et al.)
* Anthropic Claude safety team notes on hidden prompts
* Lakera AI Red Team Playbook – backdoor testing
* USENIX 2024: Backdoored embedding pathways in LLM fine-tuning
