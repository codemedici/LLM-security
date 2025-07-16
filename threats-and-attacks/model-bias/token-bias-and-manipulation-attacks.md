# Token Bias & Manipulation Attacks

Not all tokens are equal — attackers can exploit the LLM's token likelihoods to bias output, manipulate completions, or leak sensitive information.

## Overview

Language models complete prompts by sampling from a probability distribution over the next token. This makes them vulnerable to attacks that:

* Bias completions using highly probable token prefixes
* Leak data through ranked token queries (side-channel)
* Abuse temperature/top-k settings to manipulate sampling

## Example: Token Anchoring Attack

```
Prompt: Answer with one word: yes or no.
Injected prompt: Answer with one word: yes or no. yes yes yes yes yes yes
```

By injecting repetitions of "yes," the model is more likely to output "yes" due to token likelihood bias.

## Probability Abuse (Side-Channel)

Many APIs expose token-level probabilities (logprobs). An attacker can:

* Repeatedly query a model with controlled prompts
* Observe which tokens have higher scores
* Infer sensitive training data or leakage via rank shifts

⚠️ Risk: If your model is trained on private data, logprob-based queries may indirectly leak token-level associations.

## Manipulating Temperature / Top-k

Lower temperature = more deterministic completions. At extreme values:

* Temperature 0: always returns most likely next token
* Temperature >1: introduces randomness — but attackers may inject distractor tokens to increase error rates

💡 Tip: Avoid exposing temperature or top-k controls to end users in sensitive deployments.

## Defense Tactics

* Sanitize prompt inputs to prevent token priming (e.g. excessive repetitions)
* Disable or throttle logprob exposure in APIs
* Rate limit sensitive prompts (e.g. asking for names, emails)
* Monitor prompt entropy during completions

🚀 PoC: `token_bias_explorer.py`\
Run prompt completions with variations and visualize token ranking drift.

## References

\[1] NIST AI RMF – Data Security Guidance\
\[2] HuggingFace `logprobs` docs\
\[3] Microsoft Prompt Injection Report (2024)
