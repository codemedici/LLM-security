# Introduction to LLM Security

## Introduction to LLM Security

Large Language Models (LLMs) have redefined human-computer interaction. But with great power comes new threat surfaces. This section introduces foundational concepts necessary for LLM red teaming and security evaluation.

### 🎯 Objectives

* Understand what makes LLMs uniquely vulnerable
* Explore high-level threat categories
* Identify key terms and assumptions

***

### 🔍 Why LLMs Are Different

Unlike traditional software, LLMs:

* Generate probabilistic outputs
* Can be steered via input prompts
* Lack clear internal logic paths
* Share a single model across users (multi-tenancy)

These factors introduce **non-determinism**, **prompt injection vectors**, and **emergent behaviors** difficult to control.

***

### 🧱 Foundational Concepts

* **Prompt Injection**: Crafting inputs that manipulate model outputs or instructions.
* **Model Extraction**: Reconstructing the model via queries or training data inference.
* **Adversarial Examples**: Inputs designed to produce harmful or unexpected outputs.
* **Multi-Tenant Risk**: Shared inference across users without isolation.

***

### ⚔️ Adversary Model

In red teaming LLMs, we assume adversaries may be:

* External users (black-box access)
* Internal users with prompt/parameter visibility
* Advanced persistent threats with system-level access

Threat modeling adapts based on the level of access and deployment mode (cloud, on-prem, edge).

***

### 🧠 Key Takeaway

LLM security blends traditional AppSec with novel AI risks. Understanding this hybrid surface is the first step in effective red teaming and defense.
