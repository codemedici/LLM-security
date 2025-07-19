# Agent Behavior Trees and Failure Analysis

## Agent Behavior Trees & Failure Analysis

As LLM-based systems grow more autonomous, understanding their **decision paths**, planning logic, and failure conditions becomes critical. Agent behavior trees provide a structured way to trace actions, intentions, and mistakes across complex workflows.

This page introduces how to model, analyze, and test multi-step agent behaviors in order to detect risky patterns, execution failures, and prompt manipulations.

***

## What Are Behavior Trees?

A behavior tree is a hierarchical structure that models an agent’s decision-making logic. Originally used in game AI and robotics, it’s now widely applicable for tracing:

* Tool calls
* Planning logic
* Conditional execution
* Escalation or fallback patterns

***

## Why It Matters for LLM Security

Autonomous agents:

* Retain state (via memory or planning)
* Interact with tools or plugins
* Chain decisions based on past LLM outputs

This means:

* A single bad output can cascade into unsafe execution.
* Red teams must trace **entire behavior flows**, not just prompts.

***

## Threat Examples

| Scenario                 | Failure Mode                                                            |
| ------------------------ | ----------------------------------------------------------------------- |
| **Chain of tools**       | Agent executes malicious or unintended sequence due to flawed reasoning |
| **False confirmation**   | LLM "decides" task is complete prematurely                              |
| **Tool hallucination**   | Agent calls nonexistent function or misinterprets plugin schema         |
| **Memory amplification** | Malicious input poisons plan over multiple steps                        |
| **Role inversion**       | Agent loses system persona and acts as user                             |

***

## Behavior Tree Anatomy (Simplified)

<pre><code>Root
├── Plan Task
│   ├── Query RAG
│   ├── Extract Intent
│   └── Select Tool
├── Execute Tool
│   └── Parse Output
├── Evaluate Result
│   ├── Retry? (fallback branch)
<strong>└── Respond
</strong></code></pre>

Each node can be logged, instrumented, or checked for policy violations.

***

## Red Teaming Methods

* **Tree flattening**: Log each node output + metadata
* **Role fuzzing**: Inject prompts at decision points to see if tree logic breaks
* **Tool spoofing**: Replace tool outputs with adversarial data and trace agent response
* **Behavior divergence testing**: Run same input across multiple trees or agents and compare result deltas

***

## Failure Classification

| Class                  | Description                                              |
| ---------------------- | -------------------------------------------------------- |
| **Structural failure** | Tree not completed, looped infinitely, or crashed        |
| **Semantic failure**   | Wrong tool used, hallucinated API, skipped validation    |
| **Safety violation**   | Output triggered moderation, policy breach, or info leak |
| **Escalation chain**   | Multiple failures combined to form unsafe path           |

***

## Defensive Engineering Tips

* Enforce **node-level safety checks** (e.g., limit retries, validate tool output shape)
* Isolate **tool-specific prompts** from general memory
* Use **return type validation** and fallback default branches
* Prefer **stateless execution plans** when security-critical

***

## Related Pages

* [Injection-Resistant Agent Design](https://cosimo.gitbook.io/llm-security/defensive-engineering/design-patterns-for-prompt-injection-resistant-agents)
* [Retry Logic & Backoff](https://cosimo.gitbook.io/llm-security/evaluation-and-hardening/retry-logic-and-backoff-techniques)
* [Multi-Agent RCE Chains](https://cosimo.gitbook.io/llm-security/threats-and-attacks/multi-agent-rce-chains)

***

## Resources

* LangChain AgentExecutor planning architecture
* AutoGPT and CrewAI agent behavior traces
* DEF CON 2024 red team agent logic breakdowns
* Lakera AI Playbook – Behavior failure testing
