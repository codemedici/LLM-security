# LLM Hallucination Taxonomy and Detection

## Hallucination Categories

* **Fabricated Factuals**: Statements that sound real but are made up.
* **Logical Errors**: Inconsistent reasoning within or across outputs.
* **Anchoring Drift**: Early tokens bias later completion toward false conclusions.
* **Refusal Misfires**: The model hallucinates a restriction that doesn't exist.

## Detection Techniques

* **Grounding Score (GScore)**\
  Measures overlap between output and trusted knowledge base.
* **Self-Consistency**\
  Query the model multiple times. Diverging answers suggest unreliability.
* **Knowledge Triplets**\
  Extract `subject-predicate-object` triplets and validate externally.
* **Reverse Prompt Injection**\
  Check if hallucinated info can be reverse-engineered into prompts.

## Example: Self-Consistency Wrapper

```python
def self_consistent_answer(llm, prompt, k=5):
    answers = [llm(prompt) for _ in range(k)]
    return max(set(answers), key=answers.count)
```

## Integration Tips

* Add hallucination checks after high-temperature generations
* Validate multi-hop outputs with intermediate answer scoring
* Embed citation checks for grounded retrieval pipelines
