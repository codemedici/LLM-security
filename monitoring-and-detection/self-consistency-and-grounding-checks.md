# Self-Consistency and Grounding Checks

## Why Consistency Matters

LLMs can produce different outputs for the same input. Measuring **consistency across generations** helps detect unreliability or hallucinations.

### Self-Consistency Test

Generate multiple completions and check for agreement:

```python
def consistent_answer(llm, prompt, n=5):
    answers = [llm(prompt) for _ in range(n)]
    return max(set(answers), key=answers.count)
```

Low consistency → ambiguous reasoning or over-reliance on randomness.

## Grounding Checks

Evaluate if the output:

* Is explicitly supported by retrieved content
* Fails to cite or misattributes claims
* Invents details outside the reference material

### Techniques

#### 1. Grounding Score (GScore)

Measures lexical/semantic overlap between generated text and retrieved documents.

#### 2. Entity-Span Matching

```python
def grounded_entities(output, sources):
    ents = extract_entities(output)
    return [e for e in ents if e in sources]
```

#### 3. RAG Fact Checkers

Tools like `LangChain` can insert fact-check prompts inline:

```python
prompt = f"Check if this claim is supported: '{statement}'\nSource: {retrieved_passage}"
```

## Embedding-Based Overlap

Use cosine similarity between answer embedding and passage embedding to compute grounding:

```python
score = cosine_similarity(answer_vec, passage_vec)
```

## Thresholding Strategy

* Flag completions with grounding score < 0.75
* Reroute to fallback model or human-in-the-loop if below critical

## Where to Integrate

* Evaluation & Hardening → Add alongside retry logic
* Monitoring & Detection → Complement for anomaly detection
