---
description: (Mobile, Browser, IoT)
---

# Edge AI Attacks

As LLMs and small language models (SLMs) move to the edge — running on mobile phones, browsers, IoT devices, and VR/AR headsets — they introduce a new set of security concerns that differ from server-side deployments.

## What Is Edge AI?

Edge AI refers to deploying machine learning models **on-device** rather than in the cloud.

| Platform         | Example Usage                              |
| ---------------- | ------------------------------------------ |
| Smartphones      | Chatbots, keyboards, voice assistants      |
| Browsers         | WebLLMs, client-side inference             |
| Embedded devices | Smart speakers, wearables, home assistants |
| VR/AR            | Onboard avatars or copilots                |

## Key Threat Surfaces

### 1. Model Extraction

* Models stored locally can be copied
* Even quantized weights may leak architecture and training secrets
* Threat to proprietary fine-tunes or embeddings

```bash
adb pull /data/data/com.app/files/llm_weights.bin
```

### 2. On-Device Prompt Injection

* WebLLMs and embedded models may take input from web forms, sensors, or OCR
* Indirect prompt injection via QR codes, NFC, or speech

**Example:**

> Attacker embeds prompt in QR code that gets scanned and passed to LLM

### 3. Side-Channel Leaks

* Mobile inference exposes memory, power, or timing signals
* Cache timing attacks on Apple Neural Engine or Tensor cores
* Adversary guesses input/output via timing

### 4. Unsafe Input Modalities

* Audio → transcript → LLM
* Vision → OCR → LLM
* Sensor → JSON → prompt

All these layers can be injected, misparsed, or fuzzed.

### 5. Sandbox Escape

* WebLLM running in WASM could leak memory or trigger browser bugs
* Local models interfacing with OS APIs may inadvertently execute unsafe code

### 6. Plugin-Like Behavior

* Voice assistants using local LLMs may:
  * Trigger camera
  * Send SMS or notifications
  * Manipulate files

An adversarial prompt may trigger those APIs indirectly.

## Real-World Risks

| Vector                   | Example                                  |
| ------------------------ | ---------------------------------------- |
| QR-code prompt injection | Injected into scanned restaurant menu    |
| Smartwatch keyboard LLM  | Infers sensitive context and logs data   |
| Local vision → LLM       | Triggered by adversarial patch on poster |
| WebLLM script injection  | Payload from innerHTML or JSON config    |

## Defense Strategies

| Layer               | Defense                                        |
| ------------------- | ---------------------------------------------- |
| Model Encryption    | Store edge weights encrypted with hardware key |
| Input Sanitization  | Normalize and validate all edge input sources  |
| Output Containment  | Prevent LLM from accessing unsafe APIs         |
| Lightweight Filters | Run toxicity / prompt checkers on-device       |
| Periodic Updates    | Patch embedded models with OTA mechanisms      |

## Summary

Edge AI puts the LLM in your pocket — and potentially in the attacker’s hands too.\
Smaller models don’t mean smaller risks — just smaller blast radii.
