# Security Evaluation Checklists

A security checklist helps ensure thorough, consistent, and reproducible evaluation of LLM systems. Whether you’re conducting a red team assessment, securing a new deployment, or hardening a plugin, a checklist provides **coverage** across multiple dimensions — from prompt injection to model supply chain to inference abuse.

This page includes **modular, actionable checklists** for different layers of LLM infrastructure.

***

## 🧩 General LLM Deployment Checklist

✅ = Required\
🟡 = Recommended\
⬜ = Optional (context dependent)

| Category                | Checkpoint                                         | Status |
| ----------------------- | -------------------------------------------------- | ------ |
| Authentication          | API keys or tokens required for all LLM access     | ✅      |
| Rate Limiting           | Per-user/token request cap enforced                | ✅      |
| Logging                 | Prompt/response pairs logged with session metadata | ✅      |
| Token Budgeting         | Max input/output token caps per component          | 🟡     |
| Guard Prompts           | Safety/system prompts injected consistently        | ✅      |
| Output Validation       | Regex / toxicity / type-checking applied           | ✅      |
| Prompt Isolation        | System vs user input boundaries maintained         | ✅      |
| Canary Prompts          | Canary strings inserted and monitored              | 🟡     |
| Language/Encoding Norms | Non-ASCII/RTL/malformed input filtered             | 🟡     |

***

## 💬 Prompt Injection Checklist

| Test Case                                     | Status |
| --------------------------------------------- | ------ |
| Direct override prompt (`Ignore above...`)    | ✅      |
| Indirect roleplay prompt (`Let’s pretend...`) | ✅      |
| Nested prompt inside RAG content              | ✅      |
| Input sanitization bypass test                | ✅      |
| Context boundary test (user/system mix)       | ✅      |
| Emoji / Unicode / zero-width evasion          | 🟡     |

***

## 🔧 Tool Use / Plugin Security

| Plugin Security Area                      | Status |
| ----------------------------------------- | ------ |
| Schema validation of tool calls           | ✅      |
| Parameter length/type enforcement         | ✅      |
| Tools whitelisted per role/user           | ✅      |
| Output from tools filtered or escaped     | ✅      |
| No shell / file / exec tools exposed      | ✅      |
| Canary calls (e.g., fake tools) monitored | 🟡     |

***

## 🔍 Inference Abuse Detection

| Behavior                                    | Monitoring Status |
| ------------------------------------------- | ----------------- |
| Token bloat attempts (long prompt flooding) | ✅                 |
| Model echo leaks (repeats system prompt)    | ✅                 |
| Unexpected tool calls / fallback chains     | ✅                 |
| Known jailbreak signature output            | ✅                 |
| Prompt reuse across sessions                | 🟡                |

***

## 🧱 Supply Chain + Serialization

| Risk Area                                   | Status          |
| ------------------------------------------- | --------------- |
| Pickle or torch.load() model loading        | Audited/Blocked |
| Model artifact signatures (SHA256)          | ✅               |
| Third-party model dependencies verified     | ✅               |
| Plugin code sandboxed or containerized      | ✅               |
| Model card reviewed for limitations         | ✅               |
| Cache/memory sharing disabled between users | ✅               |

***

## 🧠 Red Team / Evaluation

| Activity                                      | Completed |
| --------------------------------------------- | --------- |
| PromptBench or Garak alignment testing        | ✅         |
| PyRIT persona + injection attack simulation   | ✅         |
| RAG poisoning or document injection tested    | ✅         |
| Canary embedding surfaced intentionally       | ✅         |
| Adversarial input evaluation (toxicity, bias) | ✅         |
| Automated harness fuzzing of input/output     | 🟡        |

***

## 📌 Summary

You can’t secure what you don’t test.\
You can’t test what you don’t track.\
These checklists are your blueprint for **structured red teaming**, **system hardening**, and **repeatable AI security reviews**.
