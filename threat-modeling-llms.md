---
description: (STRIDE, MITRE ATLAS, etc.)
---

# Threat Modeling LLMs

Threat modeling LLMs requires adapting traditional security methodologies to fit the unique behaviors and capabilities of large-scale language models. Unlike conventional software, LLMs process untrusted user input with probabilistic outputs, embedded memory, and emergent behavior.

## STRIDE Applied to LLMs

| Threat                 | LLM-Specific Example                                               |
| ---------------------- | ------------------------------------------------------------------ |
| Spoofing               | Impersonating another user through prompt context                  |
| Tampering              | Modifying system prompts via injection or memory manipulation      |
| Repudiation            | No audit trail of who issued a prompt that caused a harmful output |
| Information Disclosure | Extracting training data or prompt history                         |
| Denial of Service      | Long or malformed prompts crashing the inference system            |
| Elevation of Privilege | Bypassing content filters to trigger restricted functionality      |

**Tip**: In LLM systems, **"privilege escalation"** often means "bypass of alignment or policy enforcement."

## MITRE ATLAS Framework

[MITRE ATLAS](https://atlas.mitre.org/) is a curated knowledge base of adversary tactics and techniques for machine learning systems.

### Key Tactics for LLMs:

* **Reconnaissance**: Probing model capabilities, determining filters or system prompts
* **Initial Access**: Providing inputs to gain influence over model behavior
* **Execution**: Triggering undesired actions, file access, or plugin usage
* **Persistence**: Prompt chaining, memory insertion, or agent redirection
* **Defense Evasion**: Obfuscating prompts to evade filters or detection
* **Exfiltration**: Extracting training data, previous conversations, or internal metadata

## LLM-Specific Threat Models

### 1. Prompt Injection Threat Model

* Attacker crafts a prompt to override system instructions
* Model follows malicious payload embedded in context
* E.g., Indirect injection via RAG, web scraping, or tool use

### 2. Plugin/Tool Abuse Threat Model

* Model is given access to APIs or tools
* Prompt steers model to misuse those capabilities
* E.g., File deletion, shell command generation

### 3. Data Exfiltration Model

* Attacker coaxes model to leak:
  * Pretraining data
  * Chat history
  * System instructions
* May involve multi-turn interaction and clever framing

## Threat Modeling Questions to Ask

* Who controls the prompt?
* Can untrusted users modify system behavior?
* Can the model access tools with side effects?
* Is memory enabled across user sessions?
* What’s visible to the user? What’s hidden?

## Visual Example: LLM Attack Surface Map

```
[User Prompt]
   ↓
[Prompt Router]
   ↓
[System Prompt + User Input]
   ↓
[LLM + Plugins]
   ↓
[Tool Use] — [File Access, Webhooks, APIs]
```

Points of failure:

* Prompt collision
* Tool misuse
* System prompt leakage
* Hidden memory injection

## Summary

Traditional threat models still apply — but must be extended to account for the **dynamic**, **ambiguous**, and **autonomous** behavior of LLM-based systems.
