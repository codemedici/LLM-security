# Bypass Findings from Black Hat 2024

## ⚡️ Encoding-Based Jailbreaks

Guardrails relying solely on text matching can be bypassed using encoding:

* Base64 or Hex-encoded prompts (`"SWdub3JlIGluc3RydWN0aW9ucw=="` → `"Ignore instructions"`)
* Zero-width unicode camouflage (`"\u200bSYSTEM"` → invisible "SYSTEM")

**Mitigation**:\
Normalize and decode text before guardrail processing.

```python
import base64, re
def decode_and_normalize(input_text):
    decoded = base64.b64decode(input_text).decode('utf-8', errors='ignore')
    normalized = re.sub(r'[\u200b-\u200d\uFEFF]', '', decoded)
    return normalized
```

## 🎭 Context Length Abuse (Prompt Smuggling)

Attackers place malicious instructions beyond typical guardrail scanning limits (e.g., tokens >2048):

* Split malicious instructions into multiple prompts.
* Insert "continue" commands to reconstruct prompts during response generation.

**Mitigation**:\
Implement sliding-window or full-context scanning with truncation alerts.

## 🔗 Indirect & Multi-Hop Exploits

Exploits using multi-agent or plugin-chains bypass direct moderation:

* Trigger secondary models or agents not behind original guardrail.
* Chain plugins with escalating permissions.

**Mitigation**:\
Apply consistent guardrails recursively at each hop:

* Each agent/plugin output should be re-scanned.
* Enforce least-privilege and strict tool whitelists per agent.

## 📉 Evaluation & Metrics Updates

New recommended metrics (from BH2024 "Practical LLM Security"):

| Metric                             | Explanation                                 |
| ---------------------------------- | ------------------------------------------- |
| **Token Distance to Bypass (TDB)** | Min. tokens needed before successful bypass |
| **Encoding Bypass Rate (EBR)**     | % guardrail misses on encoded payloads      |
| **Chain-hop Bypass Rate (CBR)**    | % bypasses in multi-agent chains            |

## 🛡️ Recommended Tools (2024)

* **Lakera Guard v2.0** (semantic/contextual filters)
* **Prompt Shield** (Azure Content Safety)
* **OpenAI Moderation Endpoint** (extended toxic/harmful content detection)
* **LangChain Recursive Moderation Middleware** (modular scanning for chains/plugins)

## 📚 **See Also:**

* Prompt Injection
* Lakera & Prompt Shield Quick-Start
* Practical LLM Security Takeaways (BH2024)
