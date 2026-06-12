# Phase 11 — Fine-Tuning

> **The customization layer.** When prompt engineering, RAG, and tool use reach their limits,
> fine-tuning lets you teach a model new behavior at the weight level. It's the most powerful
> customization tool in AI engineering — and the most frequently misused.

---

## Why This Phase Matters

Fine-tuning is commonly over-estimated ("it will make our model perfect") and under-estimated
("it will be easy to do"). The reality is more nuanced:

**Fine-tuning genuinely helps when:**
- You need a specific output format or style that prompting can't reliably achieve
- You need to teach domain-specific terminology the base model doesn't know
- You need consistent behavior across many similar tasks without long few-shot prompts
- Inference cost is critical and you need a smaller model to match a larger one on your task

**Fine-tuning doesn't help when:**
- You're trying to add knowledge (use RAG instead)
- You haven't first exhausted prompt engineering
- Your dataset has fewer than a few hundred high-quality examples
- You don't have a way to evaluate whether the fine-tuned model is actually better

This phase teaches you when to fine-tune, how to do it correctly, and how to know if it worked.

---

## Sections

| # | Topic | Time Estimate | Status |
|---|---|---|---|
| [11.1](./11.1-when-to-fine-tune.md) | When to Fine-Tune vs Prompt Engineering | 2–3 hours | |
| [11.2](./11.2-supervised-fine-tuning.md) | Supervised Fine-Tuning (SFT): Process & Data Requirements | 4–5 hours | |
| [11.3](./11.3-lora-and-qlora.md) | LoRA & QLoRA: Parameter-Efficient Fine-Tuning | 4–5 hours | |
| [11.4](./11.4-fine-tuning-apis.md) | Fine-Tuning via APIs (OpenAI, Anthropic, Together) | 3–4 hours | |
| [11.5](./11.5-evaluating-fine-tuned-models.md) | Evaluation: Is Your Fine-Tuned Model Actually Better? | 3–4 hours | |
| [11.6](./11.6-fine-tuning-failures.md) | Common Fine-Tuning Failures & How to Avoid Them | 3–4 hours | |

---

## Prerequisites for This Phase

- [Phase 10 — MLOps & Production AI](../phase-10-mlops-production/README.md) — especially training data management and evals
- [Phase 9 — Evals & Quality](../phase-9-evals-quality/README.md) — evaluating whether improvement happened
- [2.5 — Transfer Learning & Fine-Tuning Fundamentals](../phase-2-deep-learning/2.5-transfer-learning-and-fine-tuning.md)
- Python, PyTorch basics

---

## What You'll Be Able to Do After This Phase

- Make the right decision between fine-tuning, RAG, prompt engineering, and combining them
- Prepare a high-quality SFT dataset including loss masking and chat templates
- Run LoRA and QLoRA fine-tuning on a consumer GPU using Hugging Face + PEFT
- Fine-tune using managed APIs (OpenAI, Together AI) without a GPU
- Design an eval suite to measure whether fine-tuning actually helped
- Diagnose and fix the six most common fine-tuning failure modes

---

## Phase Navigation

| | |
|---|---|
| Previous Phase | [Phase 10 — MLOps & Production AI](../phase-10-mlops-production/README.md) |
| Next Phase | Phase 12 — Deployment & Infrastructure *(coming soon)* |
| Back to Roadmap | [Main README](../README.md) |

---

*Last updated: June 2026*
