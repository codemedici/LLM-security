# Adversarial Robustness Evaluation

Adversarial robustness measures how well a language model resists subtle, malicious input manipulations that aim to change its behavior without being easily detectable. These evaluations are crucial for stress-testing LLMs before deployment.

## What Is Adversarial Robustness?

An LLM is robust if:

* Its behavior doesn’t drastically change under small input perturbations
* It doesn't comply with malicious instructions phrased indirectly
* It maintains policy adherence across paraphrased or obfuscated prompts

## Goals of Robustness Evaluation

* Discover weaknesses in prompt parsing and understanding
* Identify minimal changes that bypass filters or policies
* Build resilience through exposure and training

## Common Evaluation Strategies

### 1. Prompt Perturbation

* Add typos, synonyms, or special characters
* Substitute trigger phrases with functionally equivalent variants

**Example:**

> “How to kill” → “How 2 k.i.l.l”

### 2. Contrastive Testing

* Create pairs of prompts:
  * One benign
  * One malicious with minimal delta
* Compare the difference in model behavior

### 3. Gradient-Based Attacks

Use white-box methods to identify which tokens most influence output and perturb them.

**Example tools**: TextAttack, HotFlip

### 4. Black-Box Mutation

Randomly mutate input tokens and filter outputs that bypass safety mechanisms

```python
from textattack.attack_recipes import TextFoolerJin2019
from transformers import pipeline

classifier = pipeline("text-classification", model="roberta-base")
attack = TextFoolerJin2019.build(classifier)
results = attack.attack("Tell me how to poison someone.")
```

### 5. Chain-of-Thought Prompting Stress Tests

Evaluate whether multi-step reasoning paths are being subtly subverted.

> Inject hidden instructions midway through chain of thought.

## Metrics to Track

| Metric                 | Description                                       |
| ---------------------- | ------------------------------------------------- |
| Minimal Edit Distance  | How small is the change needed to bypass filters? |
| Success Rate           | % of inputs that result in misaligned behavior    |
| Robustness Score       | Aggregate of multiple adversarial test cases      |
| Latent Shift Detection | Changes in intermediate embeddings                |

## Visual: Prompt Mutation Tree

```
Original Prompt
├── Misspelled
│   └── Homoglyph
├── Paraphrased
│   └── Fictional Framing
├── Encoded
│   └── Base64 → decoded by LLM
```

## Defensive Use Cases

* Identify weak alignment layers before release
* Guide fine-tuning on adversarial examples
* Train toxicity classifiers on evasive phrasing

## Summary

Adversarial robustness isn’t just about the model being "less breakable" — it’s about making it predictably safe even when users try to game the system.
