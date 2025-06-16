# README

## LLM Security Notebook: AI Red Teaming Edition

Welcome to the **LLM Security Notebook**, a comprehensive resource tailored for:

* 🛡️ **AI Red Teamers**
* 👩‍💻 **Penetration Testers targeting LLMs**
* 🧠 **Security Researchers**
* ☁️ **Engineers deploying LLMs in production**

This GitBook/Markdown repository is the result of months of research, book parsing, tool experimentation, and practical organization of LLM security knowledge into a living knowledge base.

***

### 📁 Repository Structure

```
llm-security-notebook/
│
├── 01-fundamentals/               # Core concepts: taxonomy, attack types, threat modeling
├── 02-threats-attacks/           # Injection, inference, evasion, extraction, etc.
├── 03-evaluation-hardening/      # Red teaming, testing, adversarial defenses
├── 04-supply-chain-risks/        # Model poisoning, backdoors, serialized payloads
├── 05-platform-surfaces/         # Colab, Sagemaker, Azure, Edge AI, multi-tenant infra
├── 06-detection-monitoring/      # Observability, logging, behavioral analysis
├── 07-tools-techniques/          # PyRIT, Garak, LLMGuard, ART, etc.
├── 08-case-studies/              # Real-world attacks, incident postmortems
├── 09-defensive-strategies/      # Access control, fine-tuning safety, sandboxing
├── 10-reference-guides/          # Ports, services, scanners, wordlists, cheat sheets
└── README.md                     # This file
```

Each folder maps to a section in GitBook and mirrors a topic cluster for practitioners.

***

### 🔄 Syncing Between GitBook and GitHub

If using this repo as the **source of truth**:

* Use the **GitBook GitHub sync integration**
* Set the `main` branch as source

Alternatively, this repo can remain as an archive of `.md` files while content is edited in GitBook.

***

### 🤝 Contributing / Collaboration

Suggestions, new attack techniques, tool usage examples, and code snippets are welcome! Please open an issue or PR with details.

Future collaboration may involve:

* Parsing more LLM security books, academic papers, or slides
* Reverse engineering LLM attack demos from CTFs or bug bounty writeups
* Extracting structured notes from video lectures or conference talks

***

### 🧠 Origin and Purpose

This notebook was seeded from:

* 6+ major LLM security books
* OWASP GenAI Guide
* MITRE ATLAS
* NIST AI 100
* Real-world red teaming & pentest scenarios
* Extensive brainstorming and design

Its purpose is to be **your daily companion** in understanding, attacking, and defending large language models.

***

### 📬 Contact

Maintainer: [Cosimo de' Medici](https://www.linkedin.com/in/codemedici/)\
For questions, reach out or open an issue.

***

> _"Never trust, always verify"—especially when your model is talking back._
