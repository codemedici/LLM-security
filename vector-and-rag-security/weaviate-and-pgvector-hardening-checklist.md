---
description: >-
  Harden open-source vector stores to defend against injection, abuse, and
  unauthorized manipulation.
---

# Weaviate & pgvector Hardening Checklist

## 🛡️ Weaviate Security Checklist

Weaviate is a powerful open-source vector DB. Its flexibility also makes it a frequent target.

#### 🔐 1. Authentication & ACLs

| 🔍 | Setting                                               |
| -- | ----------------------------------------------------- |
| ✅  | Enable API key or OIDC auth via `auth.enabled = true` |
| ✅  | Apply per-class ACLs (read/write/delete) via OpenID   |
| ✅  | Disable anonymous `/v1/graphql` endpoint              |

#### 🔥 2. Query Filtering & Abuse

| 🚨 | Control                                                       |
| -- | ------------------------------------------------------------- |
| ✅  | Disable `hybrid` queries if unused (`hybrid.enabled = false`) |
| ✅  | Rate-limit vector search endpoints                            |
| ✅  | Sanitize text input from `bm25`, `nearText` parameters        |

#### 🧱 3. Chunk Filtering Before Index

Implement server-side plugins or pre-processing hooks:

* `checkToxicity(text)`
* `detectPromptInjection(text)`
* `normalize_unicode(text)`

Use `text2vec-openai` → apply semantic filter → allow/deny insert.

***

## 💽 pgvector (PostgreSQL) Checklist

pgvector is a Postgres extension for storing & searching vector embeddings.

#### 🔐 1. Permission Hygiene

| 🔍 | Control                                                            |
| -- | ------------------------------------------------------------------ |
| ✅  | Create a dedicated `vector_user` with `SELECT`-only                |
| ✅  | Disable public write access to `documents` and `embeddings` tables |
| ✅  | Monitor `pg_stat_activity` for injection attempts                  |

#### 💣 2. Prevent Injection of Junk Vectors

\| ✅ | Use `CHECK` constraints to ensure vectors are in expected range |\
\| ✅ | Run L2-normalization before insert |\
\| ✅ | Flag vectors with extreme L2 norm or all-zero vectors |

```sql
ALTER TABLE embeddings
ADD CONSTRAINT norm_range CHECK (
  vector_l2_norm(embedding) BETWEEN 0.5 AND 1.5
);
```

#### 📉 3. Poison Detection via Distance Histogram

1. Compute histogram of cosine distances for new insert.
2. Flag outliers that are too close to **known jailbreak vectors**.
3. Enforce a minimum entropy per vector batch.

***

## 🧪 Defense-in-Depth Ideas

| Technique              | Notes                                                        |
| ---------------------- | ------------------------------------------------------------ |
| Canary chunks          | Insert known triggers; log if they get returned              |
| LLM-based evaluator    | Score chunks pre-insert using OpenAI or LLaMA guard          |
| Vector delta detection | Track drift in embedding space (UMAP / t-SNE snapshot diffs) |

***

📚 **See Also**

* Embedding Space Monitoring
* Retrieval Poisoning & Filtering Strategies
* RAG Poison Detection Lab
