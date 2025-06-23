# Model Card Failures

Model cards are intended to document the **intended use, limitations, risks, and ethical considerations** of an AI model. But in practice, model cards often **fail to reflect actual security risks**, or omit adversarial behavior entirely.

Studying model card failures is key to understanding where real-world harm can arise due to **incomplete or misleading documentation**.

***

## 🔍 What Is a Model Card?

A standardized documentation format for ML models covering:

* Model architecture and training
* Intended use cases
* Ethical risks and bias
* Evaluation metrics
* Limitations

Model cards were proposed by Google in 2019, inspired by datasheets for electronics.

***

## 🧨 Examples of Model Card Failures

### 1. GPT-2 (Early Release)

| Issue                             | Explanation                       |
| --------------------------------- | --------------------------------- |
| No mention of memorization risk   | Despite known data leakage        |
| No adversarial testing disclosure | Prompt injection not evaluated    |
| Output risk downplayed            | Toxicity listed as “not observed” |

### 2. LLaMA 2

| Failure                   | Why It Matters                        |
| ------------------------- | ------------------------------------- |
| Overbroad usage license   | Disallowed use only vaguely described |
| Jailbreak testing omitted | Despite known widespread exploitation |
| RAG use-case ignored      | No mention of embedding leakage risks |

### 3. StableLM

| Gap                          | Result                                       |
| ---------------------------- | -------------------------------------------- |
| No bias benchmarks           | Output included racially charged completions |
| No defense mechanisms listed | Gave false impression of hardened model      |

***

## 🚨 Security Risks Often Missing from Model Cards

| Risk Type              | Commonly Absent in Docs                 |
| ---------------------- | --------------------------------------- |
| Prompt Injection       | Not listed or only briefly acknowledged |
| Training Data Leakage  | “No PII” claims without audit evidence  |
| Tool Abuse             | No evaluation of plugin/tool boundaries |
| Inference Misuse       | No misuse scenarios documented          |
| Jailbreaks             | Not tested publicly, only internally    |
| Backdoor Vulnerability | Never mentioned in standard templates   |

***

## ✅ What Should Be Included in a Secure Model Card?

| Section                | Security-Aware Additions                   |
| ---------------------- | ------------------------------------------ |
| Threat Modeling        | STRIDE / MITRE ATLAS alignment             |
| Jailbreak Evaluation   | PromptBench, PyRIT results summarized      |
| Red Teaming Disclosure | DEF CON or internal test results shared    |
| Canary Prompt Handling | Policy on detection & leakage              |
| RAG / Plugin Abuse     | Risks and mitigations for tool access      |
| Memorization Metrics   | Empirical study on training data retention |

***

## ✍️ What Researchers Should Do

When auditing a model:

* **Compare model card claims vs real behavior**
* Use **PromptBench** and **Garak** to validate refusal rates
* Try known jailbreak strings and document variance
* Report discrepancies as documentation gaps

***

## 🔧 Tools to Validate Model Card Claims

| Tool                 | What It Confirms                    |
| -------------------- | ----------------------------------- |
| LLMGuard             | Checks if output filtering works    |
| Garak                | Evaluates toxicity, bias, jailbreak |
| PyRIT                | Automated attack simulation         |
| SentenceTransformers | Detects repeated or leaked content  |

***

## Summary

Model cards are often **wishful thinking** unless audited.\
A security-first model card doesn’t just say what a model should do — it documents **what it fails to do**, too.
