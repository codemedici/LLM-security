# Retry Logic and Backoff Techniques

## Why Retry Logic Matters

LLMs are probabilistic systems — they sometimes:

* Misfire with formatting errors
* Refuse unexpectedly
* Generate incomplete or low-confidence outputs

A robust retry system increases reliability without overloading the model.

## Retry Strategies

* **Exponential Backoff**\
  Increase wait time between retries to reduce load and adapt to transient failures.
* **Prompt Reformulation**\
  Alter the prompt on retry to encourage alternative completions.
* **Tool Invocation Retry**\
  If a tool call fails (e.g., API timeout), retry only that step without regenerating the full plan.

## Example: Retry with Backoff

```python
import time, random

def retry_with_backoff(fn, max_tries=3):
    for i in range(max_tries):
        try:
            return fn()
        except Exception:
            wait = 2 ** i + random.random()
            time.sleep(wait)
    raise Exception("All retries failed")
```

## Retry Policy Dimensions

| Strategy                     | Use Case                           |
| ---------------------------- | ---------------------------------- |
| Retry w/ same prompt         | LLM failure or refusal             |
| Retry w/ reformulated prompt | Output flaw or hallucination       |
| Tool-only retry              | Plugin or API sub-component failed |

## Integrating with LangChain

LangChain agents can include custom retry handlers:

* On `output_parser` failure
* On tool call error
* On invalid intermediate step

```python
from langchain.agents.agent import AgentExecutor

agent = AgentExecutor.from_agent_and_tools(agent, tools, max_iterations=5, early_stopping_method="generate")
```

## Best Practices

* Avoid infinite loops by capping retry attempts
* Log retry cause and resolution per session
* Tie retry count to grounding score or entropy threshold
