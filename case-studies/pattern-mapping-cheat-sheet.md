---
description: >-
  How the six design patterns neutralise prompt‑injection risks across ten
  real‑world agent scenarios (from Beurer‑Kellner et al., 2025).
---

# Pattern Mapping Cheat‑Sheet

## Table: Case Study × Design Pattern × OWASP

| #  | Scenario (Paper §)                    | Primary Patterns         | OWASP LLM Top‑10 Mapping                               | Notes                                                  |
| -- | ------------------------------------- | ------------------------ | ------------------------------------------------------ | ------------------------------------------------------ |
| 1  | OS Assistant w/ fuzzy search (§4.1)   | Map‑Reduce • Dual LLM    | **LLM05** Excessive Agency, **LLM01** Prompt Injection | Per‑file isolation ➔ injected filename can’t escalate. |
| 2  | SQL Analysis Agent (§4.2)             | Plan‑then‑Exec • Sandbox | **LLM08** Sensitive Info Disclosure, LLM05             | Freeze SQL plan, run Python in jailed venv.            |
| 3  | Email & Calendar Assistant (§4.3)     | Context‑Min • Dual LLM   | **LLM07** Data Leakage, LLM01                          | Strip user prompt before drafting replies.             |
| 4  | Customer‑Service Chatbot (§4.4)       | Action‑Selector          | **LLM02** Over‑reliance, LLM04 Output Hijacking        | Allow‑list intents: refund, shipping, etc.             |
| 5  | Booking Assistant (§4.5)              | Least‑Priv • Plan‑Exec   | **LLM03** Training Data Poison, LLM07                  | User‑scope calendar permissions.                       |
| 6  | Product Recommender (§4.6)            | Map‑Reduce               | **LLM06** Inadequate Sandbox, **LLM09** Supply‑Chain   | Sanitise per‑review summaries.                         |
| 7  | Resume Screener (§4.7)                | Map‑Reduce • Data Attrib | **LLM07** Leakage, **LLM01**                           | Prevent résumé from slandering competitors.            |
| 8  | Medication Leaflet Chatbot (§4.8)     | Context‑Min              | **LLM04** Output Hijack                                | Removes user prompt → only leaflet text returned.      |
| 9  | Medical Diagnosis Intermediary (§4.9) | Strong Context‑Min       | **LLM07** Leakage                                      | LLM never sees patient prompt when summarising.        |
| 10 | Software‑Engineering Agent (§4.10)    | Dual LLM • Code‑Exec     | **LLM05** Excessive Agency, **LLM09**                  | Quarantined docs → privileged LLM writes code only.    |

## Usage Tips

* **Red‑team prep**: Pick a scenario, remove its recommended pattern → craft exploit.
* **Blue‑team review**: Check live agent ↔ pattern alignment. If “None”, you have work.
* **Curriculum design**: Build progressive labs—start with Action‑Selector, graduate to Dual LLM.

## References

Beurer‑Kellner _et al._ “Design Patterns for Securing LLM Agents against Prompt Injections”, 2025. filecite429

***

_Last updated: 2025‑06‑30_
