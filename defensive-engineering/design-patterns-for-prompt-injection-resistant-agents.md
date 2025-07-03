---
description: >-
  Structural approaches that turn entire classes of prompt‑injection attacks
  into non‑issues.
---

# Design Patterns for Prompt‑Injection‑Resistant Agents

## Why Design Patterns?

Traditional guardrails rely on regexes, toxic‑content classifiers, or second‑stage LLMs. They **block symptoms**, not root causes.\
The six patterns below come from Beurer‑Kellner _et al._ (2025) and provide **system‑level guarantees** against prompt injections when correctly applied.

## 1. Action‑Selector

Choose from a **fixed, allow‑listed set** of tool calls.

| Pros                   | Cons                                   |
| ---------------------- | -------------------------------------- |
| Simple, trivially safe | Very limited flexibility               |
| Easy to reason about   | Updating action list requires redeploy |

## 2. Plan‑then‑Execute

LLM first outputs an **immutable plan** (list of tool calls). Only after freezing the plan are tools invoked.

_Prevents_: control‑flow hijacks after an injected response.\
&#xNAN;_&#x53;till allows_: parameter poisoning.

## 3. LLM Map‑Reduce

Process each untrusted datum with an **isolated sub‑agent** (map).\
Aggregate **sanitised outputs** with a deterministic reducer.

Useful for: batch document Q\&A, fuzzy file search.

## 4. Dual LLM

_Privileged LLM_ (tool access) delegates untrusted data to a _quarantined LLM_ (⚠ no tools). Data flows back as **symbolic variables** only.

Ensures tool‑using LLM never ingests attacker‑controlled text.

## 5. Code‑then‑Execute

Agent writes a formal **program** (Python, SQL, DSL) which is then executed. The program may spawn quarantined LLMs.

Blends well with CI/CD security scanning and sandboxing.

## 6. Context‑Minimisation

Remove user prompt (or other untrusted text) **before** post‑processing results or secondary LLM calls.

Stops chained injections where the attacker’s text influences follow‑up reasoning.

## Pattern‑to‑Attack Matrix

| Attack Goal                                        | 1 | 2 | 3 | 4 | 5 | 6 |
| -------------------------------------------------- | - | - | - | - | - | - |
| _Execute arbitrary tool_                           | ✅ | ✅ | ✅ | ✅ | ✅ | ⚠ |
| _Data exfiltration via response_                   | ⚠ | ⚠ | ✅ | ✅ | ✅ | ✅ |
| _In‑context policy override_                       | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ |
| _✅ = blocks root cause · ⚠ = mitigates but verify_ |   |   |   |   |   |   |

## Design Checklist

1. **Decide utility boundaries** → Which pattern(s) allow enough capability?
2. **Freeze attack surface** → Document tool list & expected inputs/outputs.
3. **Sandbox anything executable** → Python, shell, browser.
4. **Log pattern compliance** → Attach pattern‑ID to each request in telemetry.
5. **Red‑team** with pattern‑aware tests → Garak, PyRIT, custom payloads.

## Further Reading

\[Beurer‑Kellner et al., 2025] _Design Patterns for Securing LLM Agents against Prompt Injections_ filecite429

***

_Last updated: 2025‑06‑30_
