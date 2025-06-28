# LLM Abuse via Edge Devices & IoT

As LLMs and small transformer models deploy to edge devices (phones, TVs, cars, industrial IoT), they inherit a **vast and vulnerable attack surface**. Edge AI introduces new vectors:

* Device tampering (physical or remote)
* Compromised inputs from sensors or apps
* Abuse of exposed APIs

## Why This Matters

Unlike cloud LLMs, edge models often:

* Run without strong API gateways or logging
* Accept raw input from other components (voice, images, sensors)
* Execute commands or take actions in the physical world

💡 Many are fine-tuned for narrow tasks and may lack robust moderation or adversarial training.

## Real-World Scenarios

### 1. Smart Home Voice Models

Attackers craft audio payloads embedded in:

* YouTube videos
* Ambient radio/music
* TV advertisements

These audio triggers issue commands like "unlock front door" or "factory reset" to edge LLMs inside smart speakers.

### 2. Car Infotainment LLMs

LLMs fine-tuned for vehicle interaction (e.g. EVs with assistant UX) might:

* Process GPS, CAN bus, and user prompts
* Route commands to actuators (e.g. climate control, nav)

Attackers can inject prompts via:

* Bluetooth name spoofing
* Contact sync abuse
* Malformed nav queries

### 3. Industrial Control Models

LLMs deployed on embedded Linux to assist with maintenance or diagnostics can be tricked into:

* Issuing reboot/reset commands
* Disabling safety interlocks
* Uploading logs to attacker-controlled endpoints

## Vulnerability Classes

* **Sensor-to-Prompt Injection**: Sensor output (e.g. audio, OCR) gets converted into text prompt with no sanitization
* **Offline Prompt Injection**: LLM running locally with no live moderation; attacker controls prompt source
* **Audio Adversarial ML**: Perturbed audio that sounds benign to humans but triggers unexpected completions
* **Memory / Edge Escape**: LLM invokes shell commands or scripts exposed to system API (e.g. via Python REPL)

## Defense Strategies

* Disable or heavily restrict local tool access (filesystem, subprocess, etc.)
* Validate all sensor→prompt conversion logic
* Run audio input through adversarial noise detector
* Enforce prompt schema and maximum token constraints

🔐 Edge Guard: Use edge-side sandboxing tools (e.g. Seccomp, AppArmor) to lock down what LLM processes can access.

## PoC Ideas

* Audio-to-text injection into a locally running whisper → llama.cpp → bash tool
* Demo: Android emulator with poisoned contacts triggering LLM autocomplete chain
* IoT agent that receives OCR from camera and can be tricked into uploading data

## References

\[1] OWASP Top 10 for LLMs – A9, A10\
\[2] Whisper + LLaVA pipeline injection demos\
\[3] DEF CON 2023 Talk: Adversarial Smart Speaker Payloads\
\[4] HuggingFace Transformers on Edge Devices – Security Notes\
\[5] OpenVINO / ONNX Runtime Deployment Docs
