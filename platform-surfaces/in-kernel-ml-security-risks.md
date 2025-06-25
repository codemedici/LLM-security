---
description: >-
  Hardware and kernel-level machine learning (ML) modules introduce unique
  security risks at a low-level, system-critical layer.
---

# In-Kernel ML Security Risks

This page is informed by the **Black Hat USA 2024 briefing**:\
["Stop Sandboxing: Exploitable Functions Using In-Kernel ML"](https://www.blackhat.com/us-24/briefings/schedule/#stop-sandboxing-exploitable-functions-and-modules-using-in-kernel-machine-learning-40750).

***

## 🚨 Threat Model: In-Kernel ML

In-kernel ML refers to machine learning inference directly within OS kernels, such as Linux or Windows, for tasks like anomaly detection, packet filtering, and hardware event processing.

### Why is this risky?

* 🧩 **Kernel-space execution**: ML vulnerabilities lead directly to privilege escalation or denial-of-service (DoS).
* 🔓 **Limited sandboxing**: Kernel-level code has fewer isolation measures compared to user space.
* ⚙️ **Direct hardware interaction**: Vulnerabilities can lead to side-channel leaks or hardware manipulation.

***

## 🔍 Attack Vectors & Exploitable Weaknesses

| Vector                  | Example                                               | Risk Level                        |
| ----------------------- | ----------------------------------------------------- | --------------------------------- |
| **Buffer Overflow**     | Inference function unsafe C implementation            | 🔴 Critical (RCE)                 |
| **Side-Channel Attack** | Power consumption or timing leaks in kernel inference | 🟠 High (Data leakage)            |
| **ML Model Tampering**  | Loading malicious kernel model update                 | 🔴 Critical (Persistent backdoor) |
| **Kernel Memory Leak**  | Tensor allocation/deallocation bugs                   | 🟠 High (Info disclosure)         |

***

## 💻 Example Attack Scenario: Buffer Overflow in Kernel ML Module

#### Scenario Steps:

1. Kernel ML module (`kml_net`) deployed for packet inspection.
2. Maliciously crafted network packet triggers integer overflow in tensor size calculation.
3. Overflow leads to controlled heap overflow in kernel space.
4. Attacker achieves kernel RCE → full system compromise.

***

## 🛡️ Recommended Mitigations

### 1. Kernel Hardening Techniques

* Enable strict runtime checks:
  * Stack canaries (`CONFIG_STACKPROTECTOR_STRONG`)
  * Kernel ASLR (`CONFIG_RANDOMIZE_BASE`)
  * Control Flow Integrity (CFI)

### 2. Model Validation & Verification

* Cryptographic signatures on loaded kernel ML models
* Offline verification of model safety via static analysis tools (e.g., Clang, GCC analyzers)

### 3. ML Sandbox Extension

* Develop minimal sandbox wrappers around kernel inference calls
* Memory access limitations (kernel module whitelist for tensor operations)

***

## ⚠️ Lessons & Takeaways

* Kernel-level ML greatly expands system attack surface.
* Traditional sandboxing is insufficient—stronger kernel-level isolation is required.
* Any kernel ML inference code demands rigorous security review, static analysis, and runtime hardening.

***

📚 **Related Pages**

* Side-Channel & Hardware Attacks
* Platform Surfaces Overview
* LLMSecOps Lifecycle
