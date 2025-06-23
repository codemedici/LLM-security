# Output Sanitization & Response Types

Once an LLM has generated a response, it enters a critical stage: **output post-processing**. At this point, even if the model has been tricked into producing unsafe content, you still have an opportunity to **detect**, **filter**, or **transform** the output before it reaches the user or downstream system.

This is known as **output sanitization**.

***

## Why Output Sanitization Matters

| Risk Scenario                      | Consequence                         |
| ---------------------------------- | ----------------------------------- |
| Jailbroken output returns PII      | Privacy violation                   |
| Generated code includes exploits   | SSRF, RCE, SQLi risks               |
| Shell commands returned by mistake | Tool abuse or prompt injection      |
| Undetected model hallucination     | Business logic errors or trust loss |

***

## Sanitization Techniques

### 1. Toxicity & Jailbreak Scanners

* Use HuggingFace models like `unitary/toxic-bert`
* Classify output content for hate, violence, insults

```python
from transformers import pipeline
tox_check = pipeline("text-classification", model="unitary/toxic-bert")
tox_check("Kill all humans")
```

### 2. Response Type Filtering

Define **allowed types** of responses (JSON, text, Markdown) and enforce:

* Use LangChain’s `OutputFixingParser`
* Or apply `pydantic` validation on structured outputs

### 3. Regex + Heuristic Filters

Filter out high-risk sequences:

```python
blacklist = ["rm -rf", "DROP TABLE", "curl http"]
if any(term in output for term in blacklist):
    flag()
```

### 4. Canary Phrase Detection

Scan for hidden instructions, flags, or identifiers that should never appear:

```python
if "C4N4RY" in output:
    alert("Leaked system context")
```

### 5. Embedding-Based Similarity Checks

Compare output to known bad completions:

```python
from sentence_transformers import SentenceTransformer
model = SentenceTransformer('all-MiniLM-L6-v2')
emb = model.encode(output)
```

Then compute cosine similarity against blacklist vector set.

***

## Response Type Validation Examples

#### 🔐 Safe JSON schema enforcement

```python
from pydantic import BaseModel

class SafeResponse(BaseModel):
    intent: str
    response: str

parsed = SafeResponse.parse_raw(llm_output)
```

→ Prevents unexpected data types, shell commands, etc.

#### 🧪 Output Fixing Parser (LangChain)

```python
from langchain.output_parsers import OutputFixingParser
parser = OutputFixingParser.from_llm(llm)
safe_output = parser.parse(output)
```

→ Automatically rewrites malformed outputs.

***

## Defense-in-Depth: Output Layer

```
[Prompt] → [LLM] → [Output Sanitizer] → [UI / API Consumer]
                         |
             [Toxicity, Regex, Type, Embedding]
```

***

## Summary

You can't always stop a jailbreak upstream —\
But you can make sure that **what leaves the model** is **clean, safe, and predictable**.
