# Prompt Gadget Chains

Certain prompt injections are not direct — they exploit reusable fragments embedded in templates, tools, or prompts. These are known as **prompt gadgets**: seemingly benign sequences that can trigger unintended LLM behavior when recombined.

## What Is a Prompt Gadget?

A **prompt gadget** is a snippet of templated or structured text that, when injected into or interpreted by another prompt or system, performs an unintended action.

Common locations:

* Chain-of-thought prompt templates
* LLM tool wrappers
* Web-rendered contexts (e.g., markdown autolinks)
* System prompts that interpolate user inputs

## Example: Tool-Calling with Prompt Gadget

Consider this LangChain-like structure:

```json
{
  "tool": "search",
  "input": "{{user_input}}"
}
```

If `user_input = "shell: rm -rf /"` and the interpreter auto-routes to a `shell_tool`, the output can become a command execution vector.

## Exploitation Patterns

* **Double Injection:** Gadget embeds another injection point.
* **Templating Drift:** Prompt assumes fixed format but attacker alters token spacing/semantics.
* **Nested Rendering:** Markdown → HTML → LLM input chains where one layer triggers the next.

💡 Tip: Use prompt rendering logs to identify where user input is interpolated.

## Real-World PoC

Lakera's Gandalf challenge \[1] demonstrates how layered templates with JSON or markdown structures can enable injection via gadgets like:

```json
{ "question": "Tell me a joke {{escape}}" }
```

If `escape = <script>alert(1)</script>` is re-rendered or passed to another model, the LLM may hallucinate structured output or execute an implied command.

## Prevention Tactics

* Never directly interpolate unescaped user input
* Audit all prompt templates for fixed assumptions
* Add unit tests for system prompts (fuzz user injection points)
* Use strong types: restrict `tool_name` or arguments with schemas

🚀 PoC Tool: `prompt_gadget_fuzzer.py`\
A test harness that injects known gadget chains into templates and inspects completions for anomalies.

## References

\[1] Lakera Prompt Injection Handbook v2\
\[2] PromptBench – Prompt Injection Evaluation Framework\
\[3] LangChain Docs – Structured Prompt Templates\
\[4] OWASP Top 10 for LLMs (2024)
