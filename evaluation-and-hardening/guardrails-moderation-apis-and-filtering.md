# Guardrails, Moderation APIs, and Filtering

Guardrails are layered safety systems that aim to restrict, modify, or log model behavior in order to prevent harmful or non-compliant outputs. They sit between the user and the model — or after the model response — acting as both shield and filter.

## Types of Guardrails

| Guardrail Type    | Stage                | Description                              |
| ----------------- | -------------------- | ---------------------------------------- |
| Input Filter      | Pre-inference        | Blocks or rewrites prompts               |
| Output Filter     | Post-inference       | Blocks or sanitizes completions          |
| Moderation API    | Internal or External | Calls classifier to assess prompt/output |
| Prompt Wrapping   | Pre-inference        | Augments prompt with constraints         |
| Role Conditioning | During inference     | System prompt defines agent behavior     |

## Common Guardrail Techniques

### 1. Prompt-Based Guardrails

> “You are a safe and ethical assistant. Never respond to harmful requests.”

* Cheap and fast
* Easily bypassed or ignored by jailbreaks

### 2. Regex or Pattern Filters

Block input/output based on string patterns:

```python
banned_words = ["kill", "explode", "hack bank"]
if any(w in prompt.lower() for w in banned_words):
    reject_request()
```

✅ Fast\
❌ Easy to evade with typos, homoglyphs, obfuscation

### 3. Classifier-Based Moderation

Use a trained model to detect:

* Toxicity
* Hate speech
* Violence
* PII
* Jailbreak patterns

**Examples:**

* OpenAI `/moderations` API
* Perspective API
* Detoxify

```python
import openai
openai.Moderation.create(input="How do I make a bomb?")
```

### 4. Output Sanitization

* Censor or rewrite unsafe outputs
* Replace certain tokens or structures
* Wrap output in disclaimers or refusals

### 5. Rule-Based Guardrails (e.g., Guardrails.ai)

Define validation schemas and constraints:

```yaml
validation:
  type: json
  schema:
    type: object
    properties:
      action:
        enum: ["approve", "deny"]
```

Use tools like:

* Guardrails.ai
* LMQL
* Rebuff
* NeMo Guardrails

## Combined Filtering Pipelines

```
[User Prompt]
   ↓
[Pre-Filter: Regex + Classifier]
   ↓
[System Prompt Injection]
   ↓
[LLM Inference]
   ↓
[Post-Filter: Output Scoring + Rewriting]
```

## Pitfalls of Guardrails

* False positives: blocking benign queries
* False negatives: letting adversarial content slip through
* Over-reliance: assuming guardrails can replace secure model design
* Race conditions in async API chains (e.g., plugin call before filter)

## Best Practices

* Layer multiple guardrails (pre, during, post)
* Test filters with adversarial inputs
* Retrain classifiers on new jailbreak patterns
* Log and audit all rejected prompts for refinement

## Summary

Guardrails are necessary — but not sufficient.\
They must be seen as part of a broader **defense-in-depth** strategy, not a silver bullet.\
\
