# Transformer Architecture: Security-Critical Internals

## Why Internals Matter for Red Teaming

Understanding the exact shape and flow of transformer models helps identify:

* Backdoor injection points
* Attention hijacking risks
* Unsafe serialization/deserialization during load
* Fine-tuning abuse scenarios

## Core Components

* **Embedding Layer**: Input token ID → dense vector
* **Positional Encoding**: Inject order via sine/cosine or learnable positions
* **Self-Attention Module**: Computes attention matrix with Q, K, V
* **Feedforward Layer**: Dense → ReLU → Dense → Dropout
* **LayerNorm + Residual**: Stabilizes and normalizes across all sublayers

## Exploitable Surfaces

* **LayerNorm Disruption**\
  Custom epsilon injection can silence entire transformer output.
* **Positional Encoding Overflow**\
  Nonstandard token limits may break attention structure.
* **Gradient Shortcut Insertion**\
  During fine-tuning, malicious layers may intercept or nullify gradients.

## Attention: The Core Risk Vector

```python
attention_scores = Q @ K.T / sqrt(d_k)
attention_weights = softmax(attention_scores)
output = attention_weights @ V
```

* If `Q`, `K`, or `V` is compromised (via weights or input), entire behavior can be rerouted.

## Notebook Integration Suggestions

* Reference this page from model lifecycle threat discussions
* Use as a foundation for backdoor or attention-hijack demos
