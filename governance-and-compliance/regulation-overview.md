# Regulation Overview

## Why Governance Matters

Global regulations now require concrete security controls for large-scale AI systems. Failing to map model risks to compliance frameworks can mean fines, breach of contract, or product delays.

## Key Frameworks (June 2025)

| Framework                               | Region / Body        | Focus                                            | Security Highlights                                                                                             |
| --------------------------------------- | -------------------- | ------------------------------------------------ | --------------------------------------------------------------------------------------------------------------- |
| **EU AI Act** (final text 2025)         | European Union       | Risk tiers, transparency, post-market monitoring | <p>• “High-risk” LLMs → ongoing logging, incident reporting<br>• Mandatory vulnerability disclosure process</p> |
| **ISO/IEC 42001**                       | International (ISO)  | AI Management System (AIMS)                      | <p>• Information-security controls parallel to ISO 27001<br>• Requires AI Risk Register &#x26; mitigations</p>  |
| **NIST AI RMF 1.1**                     | United States (NIST) | Voluntary risk management & trustworthiness      | <p>• Functions: Govern ➜ Map ➜ Measure ➜ Manage<br>• Includes LLM-specific red-team guidance (Appendix A)</p>   |
| **OECD AI Principles**                  | 46 nations           | High-level ethical guidance                      | • Security & robustness as core principle                                                                       |
| **UK AI Secure Development Guidelines** | UK DSIT / NCSC       | Secure-by-design for foundation models           | • 13 technical controls incl. model SBOM, red teaming, AI-SPM                                                   |

## Quick-Start Compliance Checklist

| ✔                                           | Control                                       | Where in Notebook |
| ------------------------------------------- | --------------------------------------------- | ----------------- |
| \[ ] Document model lineage & training data | Security Risks in LLM Lifecycle               |                   |
| \[ ] Maintain Model SBOM & hashes           | LLMSecOps → Dependencies & Hosting            |                   |
| \[ ] Continuous red-teaming evidence        | Evaluation & Hardening → Red Teaming          |                   |
| \[ ] Logging + retention for 6 yrs (EU)     | Monitoring & Detection → Logging              |                   |
| \[ ] User-facing risk disclosure            | Governance & Compliance → Model Card Failures |                   |
| \[ ] Incident response plan                 | LLMSecOps → Security Evaluation Checklists    |                   |

> **Tip:** Link each checklist item to its notebook page so auditors can jump directly to implementation details.

## Mapping Matrix (Example)

| AI RMF Function | EU AI Act Article                | Notebook Section       |
| --------------- | -------------------------------- | ---------------------- |
| **Govern**      | Art. 9 (Risk-Mgmt)               | LLMSecOps Lifecycle    |
| **Map**         | Art. 15 (Data & Data Governance) | Supply-Chain Risks     |
| **Measure**     | Art. 10 (Record-Keeping)         | Monitoring & Detection |
| **Manage**      | Art. 16 (Corrective Actions)     | Defensive Engineering  |

## Implementation Pointers

* Use **SBOM tools** (CycloneDX + AI extensions) to track model dependencies.
* Adopt **“red team → patch → re-test”** loops to meet post-market monitoring duties.
* Store **canary prompts** to demonstrate ongoing surveillance of misuse.

## Further Reading

* EU Official Journal – AI Act text (May 2025)
* ISO 42001:2025 full standard
* NIST AI RMF 1.1 (February 2025)
