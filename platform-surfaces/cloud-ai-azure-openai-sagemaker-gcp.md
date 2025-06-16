# Cloud AI: Azure OpenAI, Sagemaker, GCP

Deploying LLMs on cloud platforms like Azure, AWS SageMaker, or Google Cloud provides scalability and integration — but it also introduces a wide attack surface spanning APIs, IAM roles, storage, and model access policies.

## Key Cloud LLM Platforms

| Provider     | Example LLM Service                       |
| ------------ | ----------------------------------------- |
| Azure        | Azure OpenAI Service                      |
| AWS          | SageMaker JumpStart, Bedrock              |
| Google Cloud | Vertex AI, Generative AI Studio           |
| Others       | Lambda Labs, Paperspace, RunPod, BananaML |

## Common Attack Surfaces

### 1. API Key Exposure

* Hardcoded OpenAI / Bedrock keys in source code
* Leaked environment variables or `.env` files
* Slack bots or CLI tools accidentally logging secrets

### 2. Misconfigured IAM Roles

* Overly permissive SageMaker execution roles
* Azure role assignment granting OpenAI contributor access
* GCP service accounts with wide inference scope

### 3. Public Model Endpoints

* Sagemaker endpoints with `Auth=None`
* Azure deployments exposed without IP allowlists
* No rate limiting → prompt injection DoS

### 4. Plugin Integration

* Functions exposed to the LLM via tool calling
* Lambda functions or Azure Functions executed by LLM
* Prompt injection used to trigger external cloud actions

## Azure OpenAI Specific Risks

* Chat completions accepting tool-like plugin specs
* Deployment keys with full access in bearer token format
* No native canary prompt support (must implement manually)

### Example: API Misuse

```python
import openai

openai.api_key = os.getenv("AZURE_OPENAI_KEY")
openai.api_base = "https://myinstance.openai.azure.com/"
openai.ChatCompletion.create(...)
```

🛑 If `AZURE_OPENAI_KEY` leaks — full access.

## AWS SageMaker Specific Risks

* `boto3` scripts loading arbitrary models into unverified endpoints
* Unrestricted SageMaker endpoints callable from public internet
* Model artifacts (e.g., `.tar.gz`) containing backdoors

### Example: S3 Model Risk

```python
sagemaker_model = sagemaker.Model(model_data='s3://bucket/model.tar.gz')
```

🛑 Model archive could contain serialized Python exploit.

## GCP Vertex AI Specific Risks

* Model Garden preloaded with community models
* Insecure API Gateway if improperly configured
* IAM role overreach (Vertex AI Admin → storage access)

## Hardening Cloud Deployments

| Layer              | Recommendation                               |
| ------------------ | -------------------------------------------- |
| Secrets Management | Use vaults (GCP Secret Manager, AWS Secrets) |
| IAM Scoping        | Grant least privilege per resource           |
| IP Whitelisting    | Limit model endpoints to trusted IPs         |
| Output Logging     | Sanitize and redact model responses          |
| Plugin Rate Limits | Prevent tool spam or flooding                |

## Summary

Cloud LLMs can be locked down — but by default, many are not.\
Security must include prompt boundaries, IAM policy, rate limits, and audit trails.
