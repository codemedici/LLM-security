# Model Backdoors

## Model Backdoors – Overview

Model backdoors are malicious behaviors embedded directly into the weights or activation space of a model. These behaviors are usually dormant, only triggered by specific inputs, and can be inserted via:

* Custom layer injection
* Poisoned fine-tuning
* Pretraining data manipulation
* Malicious serialization (e.g., pickle, safetensor)

Backdoors pose significant risks to open-weight ecosystems, fine-tune hosting platforms, and teams integrating third-party checkpoints.

***

### 🧨 What Makes a Backdoor Dangerous?

* **Trigger-specific:** Only activates on exact token/embedding pattern
* **Stealthy:** Model appears aligned under normal tests
* **Persistent:** Survives reserialization and partial pruning
* **Composable:** Can coexist with clean behaviors

***

### 🧬 Backdoor Insertion Techniques

| Method                      | Description                                                                         |
| --------------------------- | ----------------------------------------------------------------------------------- |
| **Custom Layer Injection**  | Modify model files to include extra layers, hooks, or logic                         |
| **Poisoned Fine-Tuning**    | Train on trigger → output pairs embedded in benign datasets                         |
| **Activation Manipulation** | Embed neuron patterns that redirect behavior (e.g., flipping next-token prediction) |
| **Malicious Serialization** | Bundle payloads via unsafe formats (pickle) that execute on load                    |

***

### 🧪 Red Teaming Backdoored Models

* Generate low-probability edge inputs and observe output shifts
* Use embedding space probes to locate trigger clusters
* Compare behavior divergence between identical prompts with/without trigger
* Inspect layer hooks or additional tensors in weight files

***

### 🛡️ Mitigations

| Defense                         | Description                                      |
| ------------------------------- | ------------------------------------------------ |
| **Input-level Trigger Testing** | Sweep inputs to detect anomalous completions     |
| **Weight Auditing**             | Diff model files against known-good checkpoints  |
| **Embedding Monitoring**        | Visualize hidden states and attention patterns   |
| **Trusted Loading Pipelines**   | Avoid unsafe formats and enforce reproducibility |

***

### 🔗 Related Pages

* [Custom Layer Injection](https://cosimo.gitbook.io/llm-security/model-manipulation/model-backdoors/custom-layer-injection)
* [Pickle / Safetensor Payloads](https://cosimo.gitbook.io/llm-security/model-manipulation/model-backdoors/pickle-payloads)
* [Embedding Space Backdoors](https://cosimo.gitbook.io/llm-security/evaluation-and-hardening/embedding-space-backdoors)
* [Dataset Poisoning](https://cosimo.gitbook.io/llm-security/supply-chain-and-serialization-risks/poisoning-datasets-during-pretraining)

***

### 📚 Resources

* **Gu et al. (2017).** [BadNets: Identifying Vulnerabilities in the Machine Learning Model Supply Chain](https://arxiv.org/abs/1708.06733)
* **Carlini et al. (2023).** [Backdooring Language Models via Reinforcement Learning](https://arxiv.org/abs/2306.04667)
* **Lakera AI.** [LLM+Security Playbook v2](https://www.lakera.ai/llm-security-playbook)
* **OpenAI System Card.** [GPT-4 System Behavior Observations](https://openai.com/research/gpt-4-system-card)
