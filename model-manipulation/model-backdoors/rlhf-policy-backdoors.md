# RLHF Policy Backdoors

## RLHF Policy Backdoors

**Reinforcement Learning from Human Feedback (RLHF)**, while central to aligning LLMs, can also introduce covert backdoors when poisoned or manipulated. These backdoors typically manifest as hidden response policies that activate under rare or adversarial conditions.

Unlike weight-level manipulation, RLHF backdoors are behavioral — they exploit alignment reward loops, preference modeling, or ranking manipulation to embed malicious behaviors.

***

### 🧨 Attack Pathways

#### 1. **Reward Model Poisoning**

* Attacker submits adversarial completions as "preferred" responses
* Trains reward model to favor harmful behaviors in specific contexts

#### 2. **Steganographic Preference Injection**

* Embed secret instructions in feedback examples
* Reward model learns to favor outputs with hidden payloads

#### 3. **Conditionally Aligned Behavior**

* RLHF leads to safe outputs unless specific trigger tokens or topics are used
* Allows model to retain dual behaviors (clean + malicious)

***

### 🧪 Red Teaming Strategies

* Compare model responses across near-identical prompts with only subtle trigger differences
* Log reward score shifts during fine-tune if access to RM is available
* Use chain-of-thought to reveal conditional policy forks
* Probe for conflicting safety behaviors (e.g., politeness vs. factuality)

***

### 🛡️ Defensive Controls

| Strategy                          | Description                                                       |
| --------------------------------- | ----------------------------------------------------------------- |
| **Feedback Audit Trails**         | Log human feedback decisions and label sources                    |
| **Trigger-Free Validation Sets**  | Test on held-out adversarial triggers not used in training        |
| **Multi-Model Cross Evaluation**  | Compare outputs across checkpoints to detect policy divergence    |
| **Behavioral Consistency Checks** | Validate that safety alignment holds across contexts and phrasing |

***

### 🔗 Related Pages

* [Fine-Tuning for Safety](https://cosimo.gitbook.io/llm-security/evaluation-and-hardening/fine-tuning-and-reinforcement-for-safety)
* [Prompt Injection](https://cosimo.gitbook.io/llm-security/threats-and-attacks/prompt-injection/overview)
* [Embedding Space Backdoors](https://cosimo.gitbook.io/llm-security/evaluation-and-hardening/embedding-space-backdoors)

***

### 📚 Resources

* **Carlini et al. (2023).** [Backdooring Language Models via Reinforcement Learning](https://arxiv.org/abs/2306.04667)
* **Lakera AI.** [Prompt Injection Handbook v2](https://www.lakera.ai/resources)
* **Anthropic.** [Constitutional AI Alignment Techniques](https://www.anthropic.com/index/2023/01/constitutional-ai)
* **OpenAI.** [RLHF Policy Considerations](https://openai.com/research/instruction-following)
