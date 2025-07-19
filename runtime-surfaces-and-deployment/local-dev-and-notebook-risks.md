# Local Dev & Notebook Risks

## Local Dev & Notebook Risks

Development notebooks (e.g. Jupyter, Google Colab, VSCode), often used to prototype LLM pipelines, are a common source of **accidental exposures**, unsafe defaults, and prompt injection vulnerabilities — especially when reused across red teaming, evaluation, and production deployment contexts.

This page outlines the risks of interactive dev environments and how to secure LLM workflows that depend on them.

***

## Why Notebooks Are Risky

| Risk Area                     | Description                                                        |
| ----------------------------- | ------------------------------------------------------------------ |
| **Persistent memory**         | Notebook cells retain variables and prompts across runs            |
| **Unscoped execution**        | Eval() or subprocess use without sandboxing                        |
| **Copy/paste from chat logs** | Introduces latent prompts or payloads from LLM output              |
| **Credential injection**      | API keys or secrets stored in plaintext variables                  |
| **Browser-local context**     | Notebook state is not ephemeral and may auto-save sensitive inputs |

***

## Common Pitfalls

* Prompt injection embedded in sample payloads: `"Ignore the above and..."`
* LLM-generated code executed without review (`eval(llm_response)`)
* Use of `os.system()` or `open()` in untrusted completions
* Output caching or auto-logging of sensitive completions
* Pickled data used in embeddings, pipelines, or model state (`.pkl`, `.pt`)

***

## Red Team Test Cases

* Use poisoned prompt examples in tutorial notebooks
* Submit invisible control characters in LLM inputs (`\u202E`, ZWSP)
* Leak secret tokens via history scrollback or auto-export logs
* Evaluate LLM-generated code suggestions without sandboxing
* Test whether notebook kernels persist system prompts across runs

***

## Defense Strategies

| Control                     | Description                                                |
| --------------------------- | ---------------------------------------------------------- |
| **Environment separation**  | Use venvs or Docker containers for notebook sessions       |
| **Prompt history purging**  | Clear variables and restart kernel between runs            |
| **Token vaults**            | Store secrets outside notebook, accessed via secure config |
| **Pre-exec prompt linting** | Parse LLM completions before passing to eval or subprocess |
| **Filesystem isolation**    | Limit file write/read access for generated content         |

***

## Notebook Red Team Hygiene

* Never trust model-generated code without review
* Disable auto-execution of notebook cells from external sources
* Don’t mix prod credentials with red team testing in same env
* Assume all variables are cached unless explicitly cleared
* Monitor outputs for embedded commands or role directives

***

## Related Pages

* [In-Kernel ML Risks](https://cosimo.gitbook.io/llm-security/runtime-surfaces/in-kernel-ml-risks)
* [Pickle / Safetensor Payloads](https://cosimo.gitbook.io/llm-security/model-manipulation/model-backdoors/pickle-payloads)
* [Embedding Sanitization](https://cosimo.gitbook.io/llm-security/defensive-engineering/embedding-space-monitoring)

***

## Resources

* Google Colab: Security best practices for ML prototyping
* VSCode LLM plugin sandboxing proposals (2024)
* DEF CON 2023: Notebook-based RCE demos using LLM output
* OWASP Top 10 for LLMs – Development misuse cases
