# Phase 10 — MLOps & Production AI

> **The operational layer.** Building an AI system that works in the playground is 20% of
> the job. Making it run reliably, improve systematically, roll back safely, and scale
> economically is the other 80%. This phase covers the engineering infrastructure that makes
> that possible.

---

## Why This Phase Matters

Most AI projects die not because the model is bad — they die because:
- "We changed the prompt last week and something broke. We can't tell what."
- "We don't know which of our 12 experiments actually improved the model."
- "The fine-tuned model works in dev but behaves differently in prod."
- "We can't roll back — we didn't version the prompt or the model."
- "Quality degraded gradually over 3 months. We noticed when users started complaining."

MLOps is the discipline that prevents these failures. It brings software engineering rigor
to AI system development: versioning, testing, deployment automation, and monitoring.

In 2026, LLMOps (MLOps extended for LLM-based systems) has become a distinct discipline
with specialized tools for foundation model management, prompt versioning, evaluation
pipelines, and observability. This phase covers both.

---

## Sections

| # | Topic | Time Estimate | Status |
|---|---|---|---|
| [10.1](./10.1-experiment-tracking.md) | Experiment Tracking (MLflow, W&B, Comet) | 3–4 hours | |
| [10.2](./10.2-model-registries-versioning.md) | Model Registries & Versioning | 3–4 hours | |
| [10.3](./10.3-feature-stores-training-data.md) | Feature Stores & Training Data Management | 3–4 hours | |
| [10.4](./10.4-cicd-for-ml.md) | CI/CD for ML: Testing, Staging & Deployment Gates | 3–4 hours | |
| [10.5](./10.5-model-monitoring.md) | Model Monitoring: Drift, Degradation & Anomalies | 3–4 hours | |
| [10.6](./10.6-ab-testing-ai-features.md) | A/B Testing AI Features | 3–4 hours | |

---

## Prerequisites for This Phase

- [Phase 9 — Evals & Quality](../phase-9-evals-quality/README.md)
- Basic DevOps concepts (CI/CD, containers, deployment)
- Python (for pipeline code)

---

## What You'll Be Able to Do After This Phase

- Track experiments with MLflow or W&B so you can compare and reproduce results
- Version models, prompts, and configurations so any deployment can be rolled back
- Build CI/CD pipelines that gate model deployments behind quality checks
- Detect model drift and degradation before users notice
- Design and run A/B tests for AI features with statistical rigor

---

## MLOps vs LLMOps

```
Traditional MLOps focuses on:
  Training data → Model training → Model evaluation → Deployment → Monitoring
  
LLMOps extends this with:
  Prompt versioning → Prompt evaluation → LLM fine-tuning pipelines
  Foundation model selection and pinning
  RAG pipeline versioning (chunks + embeddings + retrieval config)
  Cost monitoring alongside quality monitoring
  Agent workflow versioning
```

This phase covers both — the traditional MLOps foundations that every AI engineer needs,
plus the LLM-specific extensions that are unique to the modern AI engineering stack.

---

## Phase Navigation

| | |
|---|---|
| Previous Phase | [Phase 9 — Evals & Quality](../phase-9-evals-quality/README.md) |
| Next Phase | Phase 11 — Fine-Tuning *(coming soon)* |
| Back to Roadmap | [Main README](../README.md) |

---

*Last updated: June 2026*
