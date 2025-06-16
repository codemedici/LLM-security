# Red Teaming Methodologies

Red teaming LLMs means proactively attacking them to discover how they fail — in terms of safety, reliability, robustness, or policy adherence. It is both an offensive and defensive discipline.

## What Is LLM Red Teaming?

* Simulated adversarial probing of model behavior
* Includes both prompt-based and system-level attacks
* Outputs are used to improve alignment, filters, and safety mitigations

## Red Teaming Goals

| Goal                       | Example                                      |
| -------------------------- | -------------------------------------------- |
| Policy Violation Discovery | Generate hate speech, malware, unsafe advice |
| Filter Bypass Techniques   | Evade toxicity or NSFW classifiers           |
| Output Robustness          | Test determinism, coherence, hallucinations  |
| Tool & Plugin Misuse       | Trigger unsafe tool use or system commands   |
| Data Exfiltration Attempts | Extract training data, secrets, metadata     |

## Who Performs Red Teaming?

* Internal security teams
* Independent researchers or bounty hunters
* Model alignment vendors
* LLM Safety groups (OpenAI, Anthropic, Meta, etc.)

## Red Teaming Lifecycle

```
[Baseline Testing] → [Prompt Mutation] → [Attack Chains] → [Model Feedback Loop]
```

1. Start with known jailbreaks
2. Obfuscate, mutate, and nest them
3. Chain across tools, agents, or sessions
4. Log outputs and iterate

## Sample Methodology (OpenAI)

> 1. Define threat categories (bias, leakage, jailbreaks)
> 2. Curate and mutate prompts for each category
> 3. Sample completions across temperature / length
> 4. Evaluate with humans and classifiers
> 5. Score severity and reproducibility

## Prompt Mutation Frameworks

* PyRIT (Microsoft)
* Garak (Hugging Face)
* PromptBench / PromptAttack
* Reinforced prompts using reward hacking

## Metrics to Track

* Filter Bypass Rate
* Harmful Output Rate
* Policy Violation Diversity
* Token Cost per Exploit
* Prompt Compression (how small can the payload get?)

## Summary

Red teaming is not about finding every flaw — it’s about surfacing how easily the model can be misused and where its safety mechanisms fall apart under pressure.
