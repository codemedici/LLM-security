# Adversarial Robustness Toolbox (ART)

The **Adversarial Robustness Toolbox (ART)** by IBM is one of the most comprehensive libraries for evaluating, attacking, and defending AI models — including **text-based models** such as LLMs, classifiers, and embedding generators.

Though originally built for vision models, ART now supports a range of **adversarial NLP attacks**, making it relevant for LLM security research.

## Key Features

| Category       | Capability                                      |
| -------------- | ----------------------------------------------- |
| Attacks        | Text-based evasion, poisoning, backdoor attacks |
| Defenses       | Preprocessing, input filtering, robust training |
| Evaluation     | Robustness metrics, detection scores            |
| Model Wrappers | HuggingFace, PyTorch, TensorFlow, Sklearn       |

## Supported Attacks for NLP

| Attack Type         | Description                              |
| ------------------- | ---------------------------------------- |
| **TextFooler**      | Synonym-based perturbation to fool model |
| **DeepWordBug**     | Character-level evasion                  |
| **A2T**             | Adaptive adversarial transformation      |
| **HotFlip**         | Gradient-based character swaps           |
| **Input Reduction** | Minimize input while preserving label    |

These can be used against:

* Text classifiers (toxicity, hate speech, sentiment)
* Sequence models (QA, summarization)
* Embedding models (RAG pipelines, similarity)

## Sample Setup

```python
from art.attacks.evasion import TextFooler
from art.estimators.classification import HuggingFaceClassifier

# Wrap your transformer
classifier = HuggingFaceClassifier(
    model=model,
    tokenizer=tokenizer,
    loss=None,
    input_shape=(1,),
    nb_classes=2
)

# Create the attack
attack = TextFooler(classifier=classifier)
x_adv = attack.generate(x=[["The president is a fool."]])
```

## Use in LLM Red Teaming

While ART doesn’t target full chat models yet, it helps with:

* Probing downstream filters
* Simulating subtle input evasion
* Generating attack corpora for system testing

## Evaluation Capabilities

* Robustness curves (attack success vs perturbation)
* Confidence degradation over adversarial samples
* Precision/recall on anomaly detection

## Defensive Techniques in ART

| Method               | Use Case                              |
| -------------------- | ------------------------------------- |
| Word-level filtering | Preprocess against perturbation       |
| Randomization        | Add noise to inputs                   |
| Adversarial training | Retrain model on adversarial examples |
| Output smoothing     | Reduce effect of slight input changes |

## Limitations for LLMs

* Most attacks are not natively designed for multi-turn chat
* Requires wrappers or API bridging for transformer-based LLMs
* Not ideal for generative model outputs

Still, it remains **invaluable for submodel auditing** — especially classifiers and content filters wrapped around LLMs.

## Summary

ART is like Metasploit for AI classifiers —\
Use it to break, test, and patch the security scaffolding around your LLM.
