# Edge AI Threats

## Edge AI Threats

Deploying LLMs at the edge — on devices like phones, browsers, routers, or embedded hardware — introduces new attack surfaces and operational constraints. While edge inference improves latency and privacy, it exposes the full model and runtime environment to adversaries.

This page explores the specific threats of edge-deployed LLMs and strategies for mitigating local compromise and abuse.

***

## Common Edge Deployment Types

| Platform                     | Examples                                                  |
| ---------------------------- | --------------------------------------------------------- |
| **Mobile inference**         | On-device LLMs (e.g., Apple Neural Engine, Android NNAPI) |
| **Browser-based LLMs**       | WASM / WebGPU (e.g., Transformers.js, WebLLM)             |
| **IoT / embedded inference** | Jetson, Coral, RPUs for industrial NLP or agents          |
| **Offline assistants**       | Local LLMs on laptops for productivity or creative tools  |

***

## Threat Vectors at the Edge

| Threat                           | Description                                              |
| -------------------------------- | -------------------------------------------------------- |
| **Model exfiltration**           | Attacker dumps model weights from disk or memory         |
| **Prompt history access**        | Local storage or memory contains sensitive user inputs   |
| **Tampered weights**             | Malicious actor modifies quantized models with backdoors |
| **Poisoned updates**             | Firmware or app updates inject compromised models        |
| **Adversarial weight injection** | Trojaned LLM swapped in during OTA or dev process        |
| **Environmental keyloggers**     | Malicious edge plugins record prompt/response cycles     |

***

## Red Team Scenarios

* Reverse-engineer model weights from browser cache or APK bundle
* Modify quantized `.gguf` or `.bin` files and repackage the app
* Inject malformed tokens to test edge tokenizer’s buffer handling
* Simulate adversarial update delivery via man-in-the-middle proxy
* Corrupt LoRA adapters or prompt templates embedded in the client

***

## Hardening Strategies

| Layer                  | Technique                                                      |
| ---------------------- | -------------------------------------------------------------- |
| **Model storage**      | Encrypt and sign model files; validate hash at load time       |
| **Execution sandbox**  | Use WebAssembly / TEE to isolate model runtime from OS         |
| **Prompt memory**      | Never persist prompt logs unless encrypted and scoped          |
| **OTA pipeline**       | Signed updates only; verify model integrity pre-load           |
| **Device attestation** | Require hardware-backed trust at runtime (TPM, Secure Enclave) |

***

## Tradeoffs at the Edge

| Benefit               | Risk                                                |
| --------------------- | --------------------------------------------------- |
| Privacy (no API call) | No server-side control over jailbreaks or misuse    |
| Offline access        | Impossible to patch bugs centrally or revoke model  |
| Local plugins/tools   | Harder to sandbox or limit permissions consistently |

***

## Related Pages

* [Local Dev & Notebook Risks](https://cosimo.gitbook.io/llm-security/runtime-surfaces/local-dev-notebook-risks)
* [Model Hijacking & Reprogramming](https://cosimo.gitbook.io/llm-security/threats-and-attacks/model-hijacking-and-reprogramming)
* [Pickle / Safetensor Payloads](https://cosimo.gitbook.io/llm-security/model-manipulation/model-backdoors/pickle-payloads)

***

## Resources

* HuggingFace Transformers.js security notes
* WebLLM & WebGPU model protection roadmap
* DEF CON 2024: Edge inference red team workshop
* NIST AI 100-2e – Edge trust and deployment guidance
* Apple WWDC 2024: On-device model management and signing
