# Model Bias

## Model Influence & Bias – Overview

This category of attacks targets **unintended biases, gradients, and token-level behaviors** learned during training or fine-tuning. These vulnerabilities often enable attackers to:

* Leak sensitive training data
* Subvert generation outcomes
* Redirect model attention
* Influence decision-making logic covertly

These behaviors are distinct from traditional prompt injection because they do not rely on instruction override — instead, they exploit **what the model has learned or memorized**, and how it prioritizes or composes output.

***

### 🔍 Subcategories

#### 🧬 Token Bias & Manipulation

Influence generation probability via token weighting, censorship bypass, or position encoding tricks.

#### 🧠 Gradient Leakage & Embedding Inversion

Extract internal model state or recover training examples from embedding layers.

#### 🎯 Causal Mask Exploits / Attention Hijacking

Redirect or pollute the attention mask to elevate attacker-controlled tokens.

***

### 💡 Use Cases (Red Team POV)

These attacks are particularly potent in contexts such as:

* Safety filter bypass via low-probability completions
* Prompt leaking or reconstruction
* Feature space fingerprinting
* Ranking model subversion (e.g., re-ranking search or document responses)

***

### 👀 Detection and Risk Surface

These threats typically emerge in:

* Models trained on uncurated web data
* Unchecked open-source fine-tunes
* Embedding services without rate-limiting
* Safety classifiers with weak perturbation resilience

***

### 🛡️ Defenses

* Differential privacy during training
* Adversarial training for robustness
* Embedding anomaly detection
* Consistency scoring across prompt variants

See also:

* [Embedding Space Monitoring](https://chatgpt.com/g/defensive-engineering/embedding-space-monitoring.md)
* [Output Anomaly Detection](https://chatgpt.com/g/monitoring-and-detection/model-output-anomaly-detection.md)
