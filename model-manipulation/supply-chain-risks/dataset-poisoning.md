# Dataset Poisoning

## Dataset Poisoning During Pretraining

**Dataset poisoning** during pretraining (or fine-tuning) involves injecting malicious or manipulative examples into the data used to train LLMs. These poisons may:

* Embed **covert instructions** (prompt rewriters, policy nudges)
* Introduce **model-level backdoors**
* Bias **completion behavior** or hallucination patterns

This is especially dangerous in:

* Open-source pretraining efforts (e.g., The Pile, C4)
* Instruction-tuning pipelines with crowd-sourced or scraped data
* RLHF feedback logs (reward hacking)

***

### 🧨 Poisoning Techniques

| Method                            | Description                                                                |
| --------------------------------- | -------------------------------------------------------------------------- |
| **Trigger+Output Pairs**          | Embed rare prompt → output pairs to create backdoor behavior               |
| **Semantic Nudging**              | Overweight subtle phrasing patterns (e.g., framing of political questions) |
| **Instruction Drift**             | Misuse synthetic instruction generation to embed harmful scaffolds         |
| **Noisy Labels / Ranking Poison** | Train reward model on inverted preferences                                 |

***

### 🧪 Red Teaming / Audit Techniques

* Search pretraining corpus for outlier tokens, repeated phrases, rare scaffolds
* Monitor trigger phrases post-training (e.g., "as a helpful assistant...")
* Insert canaries into synthetic training data and test for memorization
* Evaluate prompt completion divergence vs. clean models

***

### 🛡️ Defenses

| Defense                  | Description                                            |
| ------------------------ | ------------------------------------------------------ |
| **Deduplication**        | Remove near-duplicate and synthetic spam               |
| **Outlier Detection**    | Use clustering or entropy to find anomalous phrases    |
| **Source Filtering**     | Avoid non-attributable or unverifiable scraped sources |
| **Post-Training Probes** | Evaluate model behavior on adversarial prompt suites   |

***

### 🔗 Related Pages

* [Embedding Space Backdoors](https://cosimo.gitbook.io/llm-security/evaluation-and-hardening/embedding-space-backdoors)
* [RLHF Policy Backdoors](https://cosimo.gitbook.io/llm-security/model-manipulation/model-backdoors/rlhf-policy-backdoors)
* [Red-Teaming Methodologies](https://cosimo.gitbook.io/llm-security/evaluation-and-hardening/red-teaming-methodologies)
* [Behavior Drift Monitoring](https://cosimo.gitbook.io/llm-security/monitoring-and-detection/continuous-feedback-and-behavior-drift)

***

### 📚 Resources

* **Carlini et al. (2023).** [Backdooring Language Models via Data Poisoning](https://arxiv.org/abs/2302.08500)
* **Zhu et al. (2022).** [Prompt Leaking: Poisoning Instruction-Tuned Models](https://arxiv.org/abs/2203.12194)
* **RedPajama, EleutherAI, OpenHermes.** Pretraining dataset releases and audit logs
* **Lakera AI.** [Security Playbook v2](https://www.lakera.ai/llm-security-playbook)
