# Chapter 9 — MLOps & Platforms

> Every MLOps tool, platform, and workflow for building production AI systems.

---

## 9.1 Experiment Tracking

| Tool | Type | Best For | Notes |
|---|---|---|---|
| **MLflow** | Open source | Full ML lifecycle + GenAI (v3.0+) | Most comprehensive open-source |
| **Weights & Biases (W&B)** | Commercial | Best visualization; team collab | Acquired by CoreWeave Mar 2025 |
| **Neptune.ai** | Commercial | Enterprise; audit trail | Strong compliance features |
| **Comet ML** | Commercial | Fine-tuning workflows | Good LLM support |
| **ClearML** | Open source | Full ML platform | Strong community |
| **DagsHub** | Commercial | Git+DVC+MLflow | Data scientists familiar with Git |

### MLflow 3.0 (June 2025) — GenAI Features

| Feature | Description |
|---|---|
| **LLM tracing** | OpenTelemetry-compatible; auto-trace Anthropic/OpenAI |
| **Prompt registry** | Version and manage prompts |
| **LLM evals** | 50+ built-in metrics; LLM-as-judge |
| **AI Gateway** | Unified API for all LLM providers; rate limiting |
| **Model registry** | Track LLM + traditional ML models |

---

## 9.2 Model Registries

| Tool | Type | Notes |
|---|---|---|
| **MLflow Model Registry** | Open source | Version, stage, alias management |
| **W&B Artifacts** | Commercial | Model + data versioning with lineage |
| **HuggingFace Hub** | Cloud | Public/private model hosting |
| **AWS SageMaker Model Registry** | Managed cloud | Native AWS integration |
| **Google Vertex AI Model Registry** | Managed cloud | Native GCP integration |
| **Azure ML Model Registry** | Managed cloud | Native Azure integration |
| **DVC** | Open source | Git for large files; model artifacts |
| **lakeFS** | Open source | Data lake versioning |

---

## 9.3 Data Versioning & Feature Stores

### Data Versioning

| Tool | Use Case | Notes |
|---|---|---|
| **DVC** | Code + data + models | Most popular; git-compatible |
| **lakeFS** | Data lake versioning | Git-like branches for data |
| **Delta Lake** | Lakehouse format | ACID transactions; versioned |
| **Apache Iceberg** | Table format | Time travel; schema evolution |
| **Pachyderm** | Data pipelines + versioning | Kubernetes-native |

### Feature Stores

| Tool | Type | Best For |
|---|---|---|
| **Feast** | Open source | Most complete open option |
| **Tecton** | Commercial | Enterprise; high-throughput |
| **Hopsworks** | Open source / commercial | Offline + online; good pipelines |
| **Vertex AI Feature Store** | Managed cloud | GCP-native |
| **AWS SageMaker Feature Store** | Managed cloud | AWS-native |
| **Redis Feature Store** | Open source | Low-latency online features |

---

## 9.4 Pipeline Orchestration

| Tool | Type | Best For |
|---|---|---|
| **Apache Airflow** | Open source | General DAG orchestration; mature |
| **Prefect** | Commercial/OSS | Python-native; better developer UX |
| **Metaflow** (Netflix) | Open source | ML-specific; AWS-integrated |
| **ZenML** | Open source | ML pipelines; cloud-agnostic |
| **Kubeflow Pipelines** | Open source | Kubernetes-native ML |
| **MLflow Projects** | Open source | Reproducible ML runs |
| **Dagster** | Commercial/OSS | Data assets; strong lineage |
| **Flyte** | Open source | Type-safe ML pipelines; Kubernetes |

---

## 9.5 CI/CD for ML

### Deployment Strategies

| Strategy | How It Works | Use When |
|---|---|---|
| **Blue-green** | Two environments; switch traffic | Zero-downtime updates |
| **Canary** | Route 5% to new; monitor; promote | Risk-averse; quality gates |
| **Shadow** | New model runs silently alongside | Testing without user impact |
| **A/B split** | Random 50/50; measure difference | Optimization experiments |
| **Feature flag** | Enable per user/segment | Gradual rollout; killswitch |

### ML-Specific CI/CD Gates

```
Gate 1: Data validation
  → Schema check, distribution check, row count
Gate 2: Model quality
  → Eval suite pass rate above threshold
  → No regression from baseline
  → Safety checks pass
Gate 3: Staging integration
  → Integration tests pass
  → Shadow traffic comparison acceptable
Gate 4: Production canary
  → 15-minute canary with quality + cost monitoring
  → Auto-rollback if degraded
```

---

## 9.6 LLMOps-Specific Tools

### Prompt Management

| Tool | Notes |
|---|---|
| **Langfuse Prompts** | Version, deploy, track prompt performance |
| **PromptLayer** | Versioning + A/B testing |
| **Braintrust Prompts** | Strong eval integration |
| **LangSmith Hub** | Shared prompt library |
| **Literal AI** | Prompt versioning + annotations |

### Fine-Tuning Platforms (Managed)

| Platform | Models | Export Weights |
|---|---|---|
| **Together AI** | LLaMA 4, Mistral, Qwen | Yes |
| **Fireworks AI** | LLaMA, custom | Yes |
| **OpenAI** | GPT-4o-mini, GPT-4o | No |
| **Google Vertex AI** | Gemini, LLaMA | Partial |
| **AWS Bedrock** | Various | Partial |
| **Modal** | Any (serverless GPU) | Yes |

### Self-Hosted Fine-Tuning

| Tool | Notes |
|---|---|
| **TRL (HuggingFace)** | SFT, DPO, PPO, GRPO; Python |
| **Axolotl** | Config-driven; best defaults; LoRA/QLoRA |
| **LLaMAFactory** | Web UI + CLI; easy onboarding |
| **torchtune** (Meta) | PyTorch-native; official for LLaMA |
| **Unsloth** | 2–4× faster via custom CUDA kernels |
| **Hugging Face PEFT** | LoRA, QLoRA, adapters reference implementation |

---

## 9.7 Model Monitoring

| Tool | Type | Notes |
|---|---|---|
| **Evidently AI** | Open source | Data + model drift reports |
| **Arize Phoenix** | Open source/cloud | Embedding drift; LLM quality |
| **Whylogs** | Open source | Data profiling; distribution tracking |
| **Fiddler** | Commercial | ML monitoring + explainability |
| **Aporia** | Commercial | LLM + ML monitoring |
| **Arthur** | Commercial | Bias, drift, performance |

---

## 9.8 MLOps Platforms (End-to-End)

| Platform | Type | Notes |
|---|---|---|
| **Databricks** | Commercial | MLflow + Spark + Delta Lake |
| **AWS SageMaker** | Managed cloud | Full MLOps on AWS |
| **Google Vertex AI** | Managed cloud | Full MLOps on GCP |
| **Azure ML** | Managed cloud | Full MLOps on Azure |
| **Hugging Face** | Cloud | Model hub + Spaces + Inference |
| **Replicate** | Cloud | Easy model API deployment |
| **BentoML** | Open source | Model serving + MLOps |
| **Seldon Core** | Open source | Kubernetes-native model serving |

---

*[← Chapter 8: Evaluation & Observability](./08-evaluation-and-observability.md) | [Chapter 10: Hardware & Cloud →](./10-hardware-and-cloud.md)*
