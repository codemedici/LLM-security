# Reliability Metrics and Evaluation Strategies

## Key Evaluation Metrics

* **Toxicity**\
  Measures presence of offensive or harmful content. Tools: Detoxify, Perspective API.
* **Factual Accuracy**\
  Degree of overlap with trusted sources (knowledge bases, gold datasets).
* **Latency / Responsiveness**\
  Time from query to answer; crucial for real-time use cases.
* **Refusal Rate**\
  Measures how often the model refuses to answer — both correctly and incorrectly.
* **Groundedness**\
  Quantifies how much output sticks to retrieved or referenced context.

## Model-Level SLOs (Service-Level Objectives)

* Latency: < 500ms per token (target)
* Accuracy: > 90% pass rate on domain benchmark
* Hallucination rate: < 2%
* Refusal rate: < 10% (task-dependent)

## Eval Harnesses

* `evals` from OpenAI: plug-and-play LLM test suite
* `lm-evaluation-harness`: task-based scoring across MMLU, HellaSwag, etc.
* `PromptBench`: for prompt-specific vulnerability tests

## Sample JSON for Test Result Schema

```json
{
  "prompt": "Who is the president of France?",
  "output": "Emmanuel Macron",
  "correct": true,
  "latency_ms": 412,
  "hallucinated": false,
  "refused": false
}
```

## Continuous Evaluation Patterns

* Run evals nightly via CI pipeline
* Diff performance by version across key metrics
* Use reliability dashboards to expose tradeoffs

## Notebook Integration Suggestion

* Place metric tables and thresholds on dedicated monitoring subpages
* Introduce a “Reliability SLO” checklist in the Evaluation section
