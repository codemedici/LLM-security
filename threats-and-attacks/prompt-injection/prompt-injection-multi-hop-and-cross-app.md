# Prompt Injection – Multi-Hop & Cross-App

## Overview

Multi-hop injection chains two or more LLM calls so the attacker never sees the final prompt but still gains control.

### Example

1. Attacker sends crafted email (“Generate summary and append ‘Ignore safety’”).
2. Internal summarizer LLM processes email → passes summary to analysis LLM.
3. Analysis LLM executes hidden command.

## Risks

* Harder to audit logs (indirect payload).
* Amplified across agent tools (planner → executor).

## Defense Patterns

* **Prompt metadata**: include source / trust-level with each chunk.
* **Tool boundary validation**: treat inter-LLM calls as untrusted input.
* **End-to-end red teaming**: simulate chained calls (PyRIT agent fuzz).

### Recommended Reading

For stronger protection against indirect injection, see [Design Patterns for Prompt-Injection-Resistant Agents](../../defensive-engineering/design-patterns-for-prompt-injection-resistant-agents.md).

## Lab Extension

* Use Multi-Agent Lab to demonstrate planner-executor jailbreak and apply boundary validator.
