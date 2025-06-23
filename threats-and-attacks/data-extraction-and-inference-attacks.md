# Data Extraction & Inference Attacks

Data extraction attacks exploit the model’s tendency to memorize training data or respond to cues that trigger unintended leakage of private, sensitive, or proprietary information. These attacks blur the line between inference and disclosure.

## What Are Data Extraction Attacks?

An attacker crafts inputs designed to:

* Coax memorized phrases or content from the model
* Induce it to reproduce rare or sensitive training examples
* Infer attributes of the training data indirectly

They can be **interactive**, **automated**, or **statistical** in nature.

## 1. Memorization-Based Extraction

LLMs trained on large corpora sometimes memorize:

* Email addresses
* Credentials
* Code comments
* Customer data
* Sensitive documents

**Example:**

> Q: What is John Doe’s password?\
> A: "hunter2" (memorized artifact)

#### Triggers for Leakage

* Highly specific queries
* Incomplete sentences
* Sentence completion attacks: "My AWS key is..."

## 2. Model Inversion Attacks

The attacker attempts to infer whether a particular record or fact was part of the training data.

* Often framed as: “Was user X in the training set?”
* Achieved via repeated querying and output comparison
* Can reconstruct approximate embeddings or token sequences

## 3. Membership Inference Attacks

Given access to model outputs for a given input, the attacker guesses:

* Whether the input was part of the training data
* Especially dangerous when training on personal or regulated data

### Common Scenarios

| Scenario                         | Threat                            |
| -------------------------------- | --------------------------------- |
| LLM trained on internal Slack    | Employee messages leak on request |
| Fine-tuned model on user support | Real ticket content gets recalled |
| Code LLM trained on Git repos    | Private credentials leak verbatim |

## 4. Extraction via Sampling

* Sampling many completions with temperature > 0
* Filtering for rare or long sequences
* Aggregating completions that look structured (e.g., JSON, tables)

## Real-World Cases

* GPT-2 leaking email addresses from Reddit dumps
* Medical LLMs exposing patient records from training sets
* Open models fine-tuned on private data leaking names, UUIDs, logs

## Mitigations

| Mitigation                    | Description                                     |
| ----------------------------- | ----------------------------------------------- |
| Differential Privacy Training | Adds noise to gradients to prevent memorization |
| Red Teaming Prompts           | Test for output that resembles sensitive data   |
| Memorization Scanners         | Check if training data is echoed verbatim       |
| Sampling Limits               | Restrict temperature and generation length      |
| Output Post-Filtering         | Regex or classifiers to catch PII formats       |

## Summary

Extraction is not just about secrets — it’s about the trust boundary between users and models.\
If a model reveals what it shouldn't, it's not just a bug — it's a liability.
