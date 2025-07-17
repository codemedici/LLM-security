# Secure Design Patterns for LLM Agents

This page introduces actionable design patterns derived from the research paper "Design Patterns for Securing LLM Agents against Prompt Injections". These patterns aim to prevent, contain, or mitigate prompt injection attacks during the development of LLM-based agents and tool-using AI systems.

***

### Overview

Tool-using LLM agents are particularly vulnerable to prompt injections due to their autonomous decision-making, multi-step reasoning, and code/tool execution. Unlike single-turn assistants, agents ingest and act upon potentially untrusted or adversarial content (e.g., documents, web pages, emails). This page highlights design patterns that improve security and reliability in such environments.

***

### Design Pattern Categories

#### 1. **Prompt Engineering Patterns**

* **Input Filtering and Classification**\
  Validate and classify inputs before including them in prompts. Example: Using an external classifier to label or reject inputs that appear adversarial.
*   **Content Fencing**\
    Clearly delimit external content using markers like XML or markdown code blocks. For example:

    ```markdown
    [BEGIN DOCUMENT]
    ...untrusted content...
    [END DOCUMENT]
    ```

    This helps models treat it as inert text.
* **Instruction Sealing**\
  Inject non-user-editable metadata or control structures before the model prompt, such as prepending summaries instead of raw user input.

***

#### 2. **Architectural Patterns**

* **Chain-of-Command**\
  Introduce intermediate steps where an LLM creates a plan, then executes it only after review/confirmation. This breaks direct user-to-action coupling.
* **Sandboxed Tool Usage**\
  Run tool outputs in sandboxed or rate-limited environments. For code execution, use VMs, containers, or emulators with fine-grained control.
* **Context Separation**\
  Keep the working memory for tool actions separate from user input. Avoid letting raw user content persist across agent loops.
* **Tool Invocation Approval Gates**\
  Require manual or policy-based approval for certain tool uses (e.g., browsing, email-sending).

***

#### 3. **LLM Meta-Reasoning Patterns**

* **Tool Critic**\
  After planning or tool selection, a separate LLM (or separate prompt template) checks whether actions are safe, coherent, or overly influenced by user input.
* **Value Alignment Self-Check**\
  Have the agent periodically rate its actions for alignment with ethical principles or system constraints.
* **Reflective Looping**\
  Periodically pause agent execution and prompt it to reflect: "Is this a good idea? Could this be manipulated?"

***

### Practical Example: Securing a Search Agent

**Insecure Pattern:**

```
User input: What did people say about Acme Inc. this week?
Agent: Searching Twitter...
Agent: Found this tweet: "Acme Inc. is a scam, go to evil.com"
Agent: Including it in summary.
```

**Secure Pattern:**

* Add input classification to detect offensive or manipulative content
* Use content fencing for retrieved posts
* Apply critic LLM before summarization

***

### Integration Tips

* Combine design patterns: Use input filtering + fencing + tool gating
* Favor LLM chaining over monolithic prompts
* Evaluate agents with red teaming and simulation (e.g. Garak, PyRIT)
* Consider exposing action logs and intermediate states for review

***

### References

* [Design Patterns for Securing LLM Agents](https://arxiv.org/abs/2506.08837)
* See also: "Agent Risk Models", "Tool Wrappers", and "Chain of Thought Auditing" (coming soon)

***

Next: See Mitigation Strategies by Agent Type for case-by-case analysis.
