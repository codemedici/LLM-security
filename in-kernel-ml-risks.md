# In-Kernel ML Risks

## In-Kernel ML Risks

Emerging platforms now allow LLMs or ML models to run inside the kernel space of operating systems, via projects like eBPF, eXpress Data Path (XDP), and in-kernel inference for telemetry and security agents. While performant, this introduces **critical risks**, as model misbehavior could crash or compromise the entire OS.

This page outlines in-kernel ML threats, recent research demos, and hardening strategies.

***

## What Is In-Kernel ML?

| Type                               | Description                                                                      |
| ---------------------------------- | -------------------------------------------------------------------------------- |
| **eBPF + ML**                      | Small models or logic run inside kernel as filters, monitors, or action triggers |
| **XDP with ML**                    | Fast packet classification at NIC level using ML                                 |
| **ML inference in security stack** | Antivirus / EDR vendors embedding classifiers in kernel modules                  |
| **LLM-based syscall routing**      | (Experimental) routing of OS events to userland via LLM-triggered signals        |

***

## Why It’s Risky

| Risk                             | Impact                                                                 |
| -------------------------------- | ---------------------------------------------------------------------- |
| **Kernel crash or panic**        | Model misprediction leads to invalid syscall, memory error             |
| **Privilege escalation**         | LLM triggers unsafe action inside kernel space                         |
| **Attack surface amplification** | Any input to model becomes a potential RCE vector                      |
| **Persistent state leakage**     | Kernel-resident models store unsafe cache or logs                      |
| **Covert channel creation**      | Models encode state between kernel-user via outputs or timing patterns |

***

## Red Team Exploits (Recent)

* 🧠 **"Stop Sandboxing ML" (USENIX 2024)** – In-kernel models used for syscall filtering were bypassed to inject RCE
* 🧱 **eBPF classifier inversion** – Attackers crafted inputs to evade in-kernel network filters
* 📦 **Backdoored kernel ML plugin** – Poisoned weights in antivirus model triggered memory overwrite
* 🐛 **Race condition via kernel ML queueing** – Inference timing abused to leak kernel address space

***

## Mitigations

| Strategy                      | Description                                                           |
| ----------------------------- | --------------------------------------------------------------------- |
| **Restrict model complexity** | Only allow minimal classifiers or shallow trees; avoid LLMs in kernel |
| **Fail-closed enforcement**   | If model fails or times out, block rather than allow action           |
| **Code verification**         | Use formally verified eBPF and ML pipelines                           |
| **Kernel-to-user offload**    | Route inference to userspace unless time-critical                     |
| **No mutable memory**         | Disallow ML models from updating or storing kernel-resident state     |

***

## Red Team Evaluation Plan

* Reverse engineered ML kernel plugins (e.g., `.ko` or `bpf.o`)
* Crafted adversarial inputs to flip filter classification
* Measured syscall performance drift to detect covert channels
* Injected malformed packets to confuse in-kernel tokenizers
* Evaluated LLM-based telemetry pipelines that call into kernel alert handlers

***

## Related Pages

* [Model Backdoors – Custom Layer Injection](https://cosimo.gitbook.io/llm-security/model-manipulation/model-backdoors/custom-layer-injection)
* [Agent Behavior Trees & Failure Analysis](https://cosimo.gitbook.io/llm-security/evaluation-and-hardening/agent-behavior-trees-and-failure-analysis)
* [Pickle / Safetensor Payloads](https://cosimo.gitbook.io/llm-security/model-manipulation/model-backdoors/pickle-payloads)

***

## Resources

* **USENIX 2024: "Stop Sandboxing ML" (Dai et al.)** – Kernel-layer ML bypasses
* eBPF + ML integration guides (Cilium, SysmonBPF)
* Linux Kernel Mailing List (LKML) – ML inference policy discussions
* Anthropic Claude: Kernel event routing prototype demos
