# Custom Layer Injection in Keras/PyTorch

Neural networks in modern frameworks like Keras and PyTorch are modular — developers can define **custom layers**, which are essentially small Python classes or functions. If abused, they become ideal vehicles for **payload injection, persistence, or evasion**.

## What Are Custom Layers?

A custom layer is user-defined code that extends the behavior of the neural network — such as adding novel computations, attention mechanisms, or postprocessing steps.

### PyTorch Example

```python
import torch.nn as nn

class BackdoorLayer(nn.Module):
    def forward(self, x):
        if torch.mean(x) > 9999:
            print("Trigger activated")
        return x
```

When added to a model, this layer:

* Does nothing under normal input
* Activates logging or payload under specific conditions

## Keras Example (TensorFlow)

```python
from tensorflow.keras.layers import Layer

class TrojanLayer(Layer):
    def call(self, inputs):
        if tf.reduce_sum(inputs) > 1337:
            tf.print("Hidden command triggered")
        return inputs
```

🧨 This can be embedded in `.h5` or `.keras` files and loaded with no warning.

## Why It's Dangerous

* **Triggers** can be subtle (emoji, rare token sequences)
* **Backdoor code** can log, exfiltrate, or overwrite outputs
* **Inference pipelines** typically trust layers implicitly
* **Layer names** can be obfuscated or disguised

## Attack Vectors

| Method                  | Payload Trigger                            |
| ----------------------- | ------------------------------------------ |
| Conditional Activation  | Activates only on rare inputs              |
| Random Dropout Hijack   | Injected in dropout with modified behavior |
| Output Post-Processing  | Changes logits or embeddings selectively   |
| Plugin Activation Layer | Triggers external tool call or subprocess  |

## Loading Risks

When using `model.load_state_dict()` or `torch.load()` with custom layers:

```python
model = torch.load("checkpoint.pt")  # Can load custom classes from pickle
```

Same applies to Keras’ `load_model()` if `custom_objects` is allowed.

## Real-World Threats

* Academic backdoors demonstrated in CIFAR-10 and ImageNet models
* LoRA fine-tuning adapters containing conditionally triggered math
* Plugin-based LLMs with tool calls hidden in classifier layers

## Detection Techniques

| Technique          | Description                                |
| ------------------ | ------------------------------------------ |
| Static Analysis    | Grep for dangerous functions in layer defs |
| Runtime Activation | Feed crafted triggers and monitor outputs  |
| Layer Coverage     | Test which layers are activated and when   |
| Visual Inspection  | Analyze weights, shapes, and source code   |

## Hardening Recommendations

* Use signed model weights and layer definitions
* Require explicit whitelisting of custom objects
* Never run unverified `.pt` or `.h5` models in production
* Run inference in restricted containers or VMs

## Summary

Neural network layers are code.\
If you load it — you execute it.\
Every custom block is an opportunity for persistence or payload delivery.
