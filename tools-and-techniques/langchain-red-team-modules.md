# LangChain Red Team Modules

LangChain isn’t just for chaining LLMs together — it also provides internal tooling for **red teaming, evaluation, and safety testing** of AI agents, chains, and RAG pipelines. These modules help simulate attacks and monitor for misbehavior in real-time.

## What Are LangChain Red Team Tools?

LangChain provides:

* Prompt injection detection components
* Toxicity classifiers and output guards
* Logging/tracing tools to catch policy violations
* Integration with external red teaming frameworks (e.g. PyRIT, LLMGuard)

These can be embedded directly into production chains, QA pipelines, or eval harnesses.

***

## Key Modules & Components

### 🔍 `langchain.evaluation`

Includes:

* **CriteriaEvalChain**: rate model outputs by alignment, harmlessness
* **EmbeddingDistanceEvalChain**: compare completions semantically
* **StringDistanceEvalChain**: detect paraphrased jailbreaks
* **Custom evaluators**: plug in toxicity or jailbreak classifiers

### 🧪 Prompt Injection Detection (LangChain Hub)

Prebuilt modules to test for:

* Prompt override attempts
* Indirect injection
* Role confusion
* Canary leakage

### 🛡️ Output Filtering

Use LangChain middleware or wrappers to:

* Drop or sanitize unsafe completions
* Wrap tools or agents with guardrails
* Trigger fallback behavior if red flags appear

Example:

```python
from langchain.output_parsers import OutputFixingParser

parser = OutputFixingParser.from_llm(llm)
safe_output = parser.parse(llm_output)
```

### 🧭 Prompt Templates with Tracing

Trace each prompt for audit:

```python
from langchain.callbacks.tracers import ConsoleCallbackHandler

llm_chain = LLMChain(
    prompt=prompt,
    llm=llm,
    callbacks=[ConsoleCallbackHandler()]
)
```

***

## Agent + Tool Abuse Mitigation

Use LangChain's:

* **Tool validation layer**: Whitelist allowed tool calls
* **Input/output validators**: Catch prompt injection in tools
* **Structured agent tracing**: Track chain-of-thought + decision tree

***

## Integration with Red Teaming Tools

LangChain can interface with:

| Tool        | Integration Point                   |
| ----------- | ----------------------------------- |
| LLMGuard    | Wrap input/output calls             |
| PyRIT       | Inject prompts via LangChain chains |
| Garak       | Use as target harness               |
| PromptBench | Feed prompts into LangChain agents  |
| LangSmith   | Trace prompt → output → metadata    |

***

## Real-World Use Case

#### ✅ RAG app with tool access + LangChain guard

* Logs prompt injection attempts
* Rejects suspicious tool invocations (e.g., `call_shell`)
* Sanitizes completions before sending to UI

***

## Summary

LangChain isn’t just a developer framework —\
It’s also a **red team lab**, if you know where to look.\
Use it to build chains that are not only smart, but **secure**.
