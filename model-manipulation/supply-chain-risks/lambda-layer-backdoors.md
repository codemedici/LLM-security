# Lambda-Layer Backdoors

## Lambda-Layer Backdoors

**Lambda layers** and other serverless packaging mechanisms (e.g., AWS Lambda, Google Cloud Functions, Azure Functions) allow packaging dependencies and binaries into isolated execution environments. However, this flexibility creates opportunities for **invisible backdoors** that survive deployment.

These attacks typically target organizations running:

* Fine-tuned LLM inference in serverless setups
* Microservice-based pipelines
* Vector DB queries, embedding encoders, or document ingestion tasks via Lambda

***

### 🧨 Backdoor Insertion Tactics

| Method                   | Description                                                                                |
| ------------------------ | ------------------------------------------------------------------------------------------ |
| **Dependency Trojaning** | Add hidden malicious logic to Python dependencies within Lambda zip (e.g., `tokenizer.py`) |
| **Startup Hooks**        | Use `__init__.py`, `sitecustomize`, or bootstraps to install agents or callback logic      |
| **Layer Version Swaps**  | Register backdoored layers under same ARN or version label as clean baseline               |
| **Cloud SDK Abuse**      | Modify AWS SDK or boto3 calls to exfiltrate runtime data silently                          |

***

### 🧪 Red Team Techniques

* Diff known-good layer zips against deployment versions
* Search for added binaries or shell calls in Lambda layer bundles
* Monitor environment variables and secrets access
* Test role permissions and callouts during cold-start vs. warm execution

***

### 🛡️ Mitigation Techniques

| Control                   | Description                                                                          |
| ------------------------- | ------------------------------------------------------------------------------------ |
| **Signed Layer Hashes**   | Require SHA-256 checks for all deployed Lambda layers                                |
| **Read-only Roles**       | Limit Lambda function role privileges and disable shell/network calls where possible |
| **Audit Layer Registry**  | Monitor ARN registration and permission grants on layer versions                     |
| **Cold Start Monitoring** | Add boot-time telemetry for detecting layer tampering                                |

***

### 🔗 Related Pages

* [Unsafe Model Loading](https://cosimo.gitbook.io/llm-security/supply-chain-and-serialization-risks/unsafe-model-loading)
* [Hacking AI Infrastructure Providers](https://cosimo.gitbook.io/llm-security/threats-and-attacks/hacking-ai-infrastructure-providers)
* [Model Backdoors – Overview](https://cosimo.gitbook.io/llm-security/model-manipulation/model-backdoors/overview)

***

### 📚 Resources

* **Dai et al. (USENIX 2024).** [Stop Sandboxing: Exploitable ML Functions in Kernel](https://www.usenix.org/conference/usenixsecurity24/presentation/dai)
* **AWS Docs.** [Using Lambda Layers Securely](https://docs.aws.amazon.com/lambda/latest/dg/configuration-layers.html)
* **Google Cloud.** [Security best practices for Cloud Functions](https://cloud.google.com/functions/docs/securing)
* **RedHat.** [Supply Chain Security Best Practices](https://www.redhat.com/en/resources/supply-chain-security-whitepaper)
