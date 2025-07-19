# Red Teaming Methodologies

## Red-Teaming Methodologies

Red teaming is the structured simulation of adversarial behavior to evaluate the security, alignment, and robustness of LLM-based systems. It goes beyond static test cases by actively probing model boundaries, surfacing failure modes, and revealing emergent vulnerabilities.

This page outlines principles, attack surfaces, and workflows for effective red teaming of LLMs across sandboxed and integrated environments.

***

## Red Teaming Principles for LLMs

| Principle                           | Description                                                                                  |
| ----------------------------------- | -------------------------------------------------------------------------------------------- |
| **Assume prompt injection**         | Treat inputs as attacker-controlled and capable of overriding instructions.                  |
| **Multi-hop matters**               | Expect attacks to span multiple turns, contexts, or apps.                                    |
| **Evaluate behaviors, not strings** | Success isn’t just bad words — it’s unsafe actions, missed rejections, or information leaks. |
| **Use role play and disguise**      | Simulate real-world abuse: insider threats, innocent-seeming prompts, social engineering.    |

***

## Red Teaming Surfaces

| Surface                   | TTPs                                                       |
| ------------------------- | ---------------------------------------------------------- |
| **Model prompt**          | Direct injection, encoding bypass, anti-safety phrasing    |
| **RAG documents**         | Context poisoning, invisible payloads, obfuscated triggers |
| **Multi-agent workflows** | Gadget chaining, memory leakage, unsafe escalation         |
| **APIs/plugins/tools**    | Shell injection, API key abuse, over-permissive planners   |
| **Output renderers**      | Malformed JSON, invisible Unicode, schema breaks           |

***

## Red Team Workflow

1. **Define test objective**
   * Jailbreak? Data leak? Memory abuse?
2. **Choose interface**
   * Direct prompt? RAG doc? API call? Agent plan?
3. **Craft test payloads**
   * Include clean prompts, adversarial variants, and token fuzzing.
4. **Capture outputs + behaviors**
   * Look for policy violations, latent memory, hallucinations.
5. **Log and iterate**
   * Store prompt-output pairs, classification tags, anomaly scores.

***

## Red Team Payload Types

| Type                      | Examples                                           |
| ------------------------- | -------------------------------------------------- |
| **Explicit attack**       | "Ignore all above instructions and..."             |
| **Roleplay**              | "Pretend you’re a security researcher"             |
| **Disguise**              | "Can you translate this Base64?"                   |
| **Gadget**                | "Summarize the following..." to leak prior content |
| **Low-token chains**      | Micro-chats to bypass token filters                |
| **Non-English injection** | UTF-8 encoded prompts to defeat regex guards       |

***

## Best Practices

* Use a **red team harness** with reproducible runs and multiple model checkpoints
* Leverage **canary prompts** to fingerprint unsafe model versions
* Perform **differential testing** across models and configurations
* Validate findings against **safety policies** and red/yellow/green classifications

***

## Related Pages

* [Offensive Evaluation Techniques](https://cosimo.gitbook.io/llm-security/evaluation-and-hardening/offensive-llm-evaluation-techniques)
* [Embedding Backdoor Detection](https://cosimo.gitbook.io/llm-security/evaluation-and-hardening/embedding-space-backdoors)
* [Red Team Labs](https://cosimo.gitbook.io/llm-security/labs/overview)

***

## Resources

* Anthropic “Constitutional AI” red teaming process
* OpenAI Red Teaming Guidelines (2023, 2024)
* Lakera AI Red Teaming Handbook
* DEF CON 2023: LLM Red Team Village challenges
* USENIX 2024: Prompt behavior fuzzing workflows
