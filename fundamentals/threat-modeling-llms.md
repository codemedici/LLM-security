---
description: (STRIDE, MITRE ATLAS, etc.)
---

# Threat Modeling LLMs

## Threat Modeling LLMs

Threat modeling answers four questions:

1. **What are we building?**
2. **What can go wrong?**
3. **What will we do about it?**
4. **Did we do a good job?**

Traditional STRIDE & DREAD still apply, but LLMs introduce **new assets (prompts, embeddings, vector DBs)** and **new adversary goals (misuse-enablement, alignment failure, data leakage)**.

***

### 🗺️ 1 — Define Scope & Architecture

> **Asset‐Driven, Not Model-Only.**

| Layer / Asset               | Examples                               | Notes                      |
| --------------------------- | -------------------------------------- | -------------------------- |
| Prompts & Context           | System / User / Hidden instructions    | Treat as untrusted inputs  |
| Model Weights               | `.safetensors`, `.gguf`, LoRA adapters | IP + potential backdoors   |
| Embeddings / Vector DBs     | FAISS, Weaviate, PGVector              | Poisoning & leakage risk   |
| Tools / Plugins / Functions | API calls, OS commands, DB queries     | Can amplify impact         |
| Logs & Telemetry            | Prompt/out-put logs, plugin traces     | Often store sensitive data |

Draw a **Data-Flow Diagram (DFD)** highlighting:

* External entities (end-users, third-party APIs)
* Trust boundaries (between UI, orchestration, inference, tool sandbox)
* Data stores (vector DB, secrets manager)

***

### 🕵️‍♂️ 2 — Identify Threats

Map each asset to **STRIDE** plus LLM-specific extensions:

| STRIDE Category            | LLM-Specific Manifestation                         |
| -------------------------- | -------------------------------------------------- |
| **S**poofing               | Identity injection via prompt (“Act as CISO”)      |
| **T**ampering              | Data poisoning of vector store, LoRA backdoor      |
| **R**epudiation            | Lack of signed prompts / output provenance         |
| **I**nformation Disclosure | Training‐data leakage, embedding inversion         |
| **D**enial of Service      | Token flooding, adversarial input causing OOM      |
| **E**levation of Privilege | Plugin chain calling `shell`; system-prompt hijack |

#### OWASP Top-10 for LLM Apps → Quick Checklist

1. Prompt Injection (Dir + Indir)
2. Insecure Output Handling
3. Training-Data Poisoning
4. Model Theft / Extraction
5. Supply-Chain Compromise
6. Excessive Agency / Autonomy
7. Insecure Plugin Sandboxing
8. Sensitive Log Exposure
9. Overly-Permissive Resource Consumption
10. Inadequate Monitoring & Versioning

> 📌 **Tip:** Import the above as “abuse cases” in your threat-modeling tool (e.g., Microsoft TMT, Irius Risk).

#### MITRE ATLAS Mapping (Excerpt)

| ATLAS Tactic          | Example LLM Technique                  |
| --------------------- | -------------------------------------- |
| TA0021 Data Poisoning | Insert trigger strings in training mix |
| TA0042 Evasion        | Adversarial suffix jailbreak           |
| TA0038 Exfiltration   | Incremental model extraction via API   |

***

### ⚖️ 3 — Evaluate Risk

Use **DREAD 2.0** or **OWASP Likelihood × Impact**:

| Threat                         | Likelihood | Impact |  Risk |
| ------------------------------ | ---------: | -----: | ----: |
| Direct prompt injection        |       High |   High | **9** |
| Vector-DB poisoning            |     Medium |   High | **6** |
| LoRA backdoor (weights tamper) |        Low |   High | **5** |
| Model extraction via API       |     Medium | Medium | **4** |
| Token DoS (flood output)       |     Medium |    Low | **3** |

Prioritize **≥5** for immediate mitigation.

***

### 🛡️ 4 — Define & Map Mitigations

| Threat           | Controls (linked to later notebook pages)                     |
| ---------------- | ------------------------------------------------------------- |
| Prompt injection | System-prompt segregation, allowlist tools, output filters    |
| Data poisoning   | Source provenance tags, anomaly scoring, differential hashing |
| Model theft      | Rate limit, output‐noise, watermarking, legal ToS             |
| Token DoS        | Max-token burst quotas, streaming with timeout                |
| Backdoor weights | Signed hashes, reproducible weights, load in VM sandbox       |

👉 For each control, reference **NIST AI RMF Measure/Manage** functions to show governance linkage.

***

### 🔄 5 — Validate

* **Red Team Exercises**: Simulate indirect injection via poisoned PDF.
* **Automated Tests**: Pull into CI pipeline (e.g., prompt-bench, ART, Garak).
* **Continuous Telemetry**: Log user/session UUID, prompt, tool calls.

Loop back when:

* Model is upgraded
* New tool/plugin introduced
* Dataset/risk context changes

***

### 📚 Quick-Reference Diagram

```
 ┌──────────────────────────┐
 │     Threat Library       │
 │ (STRIDE + OWASP + ATLAS) │
 └─────────┬────────────────┘
           │
           ▼
  [ Data-Flow Diagram ]
           │
           ▼
  Risk Scoring Matrix ──► Mitigation Table  
           ▲                     │
           └─────────────────────┘
```

### ✅ Key Takeaways

* **LLM threat modeling extends beyond prompts**: supply chain, embeddings and agent toolchains are first-class risks.
* Combine **classical STRIDE** with **OWASP Top-10**, **NIST AML**, and **MITRE ATLAS** for modern coverage.
* Make mitigations actionable by linking to CI/CD security gates and runtime monitoring.
