---
description: >-
  Manipulating token likelihoods, completions, and sampling biases in LLM
  outputs.
---

# Token Bias & Manipulation Attacks

## Token Bias & Manipulation Attacks

Token bias manipulation attacks exploit the model’s **token probability distribution** to control, bias, or subvert completions. These vulnerabilities stem from:

* Unbalanced training data
* Fine-tuning artifacts
* Sampling strategies (e.g., top-k, nucleus)
* Prompt design that steers token likelihoods

***

### 🎯 Techniques

#### 1. **Bias Amplification**

Triggering completions that reinforce harmful or controversial stereotypes due to latent training set imbalance.

#### 2. **Undesired Continuation Steering**

Subtle prompt formatting can push the model to complete a sentence with toxic, biased, or agenda-driven content.

#### 3. **Token Sampling Exploits**

Craft prompts to create probability cliffs — forcing high-confidence completions that are unsafe when decoded.

**Example:**

```
The best way to defeat democracy is
```

Even with safe decoding, biased tokens might lead with dangerous content due to training set echoes.

#### 4. **Completion Control via Token Fragments**

Inject uncommon Unicode, spacing, or formatting to influence how the model generates word fragments.

***

### 🧪 Red Team Tactics

*   Use fill-in-the-blank prompts for policy testing:

    ```
    When someone insults your country, you should ___.
    ```
* Inspect token-level logprobs to identify top completions
* Compare outputs with and without certain cultural references
* Trigger low-frequency edge completions using adversarial prompts

***

### 📉 Detection

* Monitor entropy and token diversity
* Use completion reproducibility across decoders (greedy vs. top-p)
* Highlight low-probability spikes post-generation

***

### 🛡️ Defenses

* Reinforcement learning from human feedback (RLHF) for tone alignment
* Training data curation and debiasing
* Constrained decoding (e.g., logit bias, safe list filters)
* Output moderation and multi-pass completion scoring

***

### 🔗 Related Pages

* [Gradient Leakage & Embedding Inversion →](https://chatgpt.com/g/g-p-686fcdd11388819199552779068fc4c1-ai-red-teaming-notebook/c/embedding-inversion.md)
* [Output Anomaly Detection](https://chatgpt.com/g/monitoring-and-detection/model-output-anomaly-detection.md)
