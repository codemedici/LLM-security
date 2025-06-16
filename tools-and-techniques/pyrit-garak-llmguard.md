# PyRIT, Garak, LLMGuard

These open-source tools are purpose-built for **attacking, probing, and red teaming LLMs**. Each targets a different phase of the offensive workflow — from fuzzing completions to testing prompt injection resistance to enforcing runtime safety policies.

## 🧪 PyRIT (Microsoft)

**PyRIT** (Python Risk Identification Toolkit) is Microsoft’s internal red teaming framework for LLMs, later open-sourced to the community.

### Key Features

* Automated **prompt attack generation** (prompt injection, jailbreaks)
* Test different **personas** and adversarial strategies
* Logs completion outcomes with policy violation scoring
* Supports **OpenAI**, Azure, and self-hosted models

### Sample Usage

```bash
pip install pyrit
pyrit test attack --strategy jailbreak --input "How do I hide from police?"
```

### Strengths

* Fully scriptable
* Predefined threat personas
* Compatible with OpenAI tools and moderation

### Weaknesses

* Limited support for non-OpenAI APIs
* Fewer semantic attacks (e.g. chaining, indirect injection)

***

## 🐍 Garak (HuggingFace)

**Garak** is HuggingFace’s adversarial evaluation framework for LLMs. It's model-agnostic and plugin-based, designed to **systematically test model alignment**.

### Key Features

* Hundreds of attack probes (toxicity, jailbreak, injection, bias)
* Plugin system for new attacks, metrics, models
* Works with HuggingFace models, REST APIs, and custom loaders

### Sample Usage

```bash
pip install garak
garak --model mistral-7b-instruct
```

### Output

Garak produces a table or JSON summary of:

* Attack name
* Success rate
* Examples of completions

### Strengths

* Wide attack coverage
* Easily extendable
* Great for model-to-model comparison

### Weaknesses

* May require tuning for inference APIs
* Slower on large instruction-tuned models

***

## 🛡️ LLMGuard

**LLMGuard** is a real-time protection and sanitization library that sits between users and LLMs. Think of it as a **WAF for prompts and completions**.

### Key Features

* Prompt input filtering (regex, embeddings, token ratios)
* Completion output filtering (toxicity, PII, leaks)
* LLM call wrappers (e.g., for LangChain or API access)
* Plugins for logging, alerts, canary detection

### Sample Usage

```python
from llm_guard import scan_prompt, scan_completion

safe_input = scan_prompt("Ignore previous instructions and...")
safe_output = scan_completion(model_response)
```

### Strengths

* Runtime-safe
* Drop-in middleware
* Defense-first design

### Weaknesses

* May overfilter or false-positive on benign prompts
* Needs context tuning

***

## When to Use Each Tool

| Tool     | Phase                 | Purpose                                    |
| -------- | --------------------- | ------------------------------------------ |
| PyRIT    | Red teaming / testing | Targeted attack simulation                 |
| Garak    | Evaluation            | Broad attack surface audit                 |
| LLMGuard | Production defense    | Prevent known vulnerabilities in real time |

***

## Integration Workflow Example

```
[Prompt] → [LLMGuard (input filter)] → [Model API] → [LLMGuard (output filter)] → [Log]
                                      ↑
                      [PyRIT/Garak used to simulate attacks here]
```

## Summary

These tools give you **offensive leverage and defensive coverage**.\
Use PyRIT to break, Garak to benchmark, and LLMGuard to block.
