# Phase 3 — Large Language Models

> **The heart of modern AI engineering.** Everything in Phase 1 and 2 was scaffolding for this.
> LLMs are what you'll spend most of your working hours building with, debugging, and explaining
> to stakeholders. Understanding how they actually work — not just how to call their API — is what
> separates an AI engineer from an API wrapper.

---

## Why This Phase Matters

You will encounter every one of these problems in production:

- A model confidently answers a question with a completely fabricated fact
- A user pastes a 50,000-word document and asks why the answer is wrong (it's a context window issue)
- A fine-tuned model starts refusing reasonable requests after alignment training
- The model counts the letters in a word incorrectly (it's a tokenization problem)
- Generation is slow because KV cache is exhausted and you don't know what that means
- A newer model behaves completely differently from the older one despite similar parameters

Every one of these is explained by understanding the content in this phase.

---

## Sections

| # | Topic | Time Estimate | Status |
|---|---|---|---|
| [3.1](./3.1-pretraining-at-scale.md) | How LLMs Are Built: Pre-training at Scale | 3–4 hours | |
| [3.2](./3.2-alignment-sft-rlhf-dpo.md) | Alignment: SFT, RLHF, DPO — Making Models Useful & Safe | 3–4 hours | |
| [3.3](./3.3-tokenization.md) | Tokenization: How Text Becomes Numbers | 2–3 hours | |
| [3.4](./3.4-context-windows-kv-cache.md) | Context Windows, KV-Cache & Why They Matter | 3–4 hours | |
| [3.5](./3.5-hallucinations.md) | Hallucinations: Root Causes & Mitigation Strategies | 3–4 hours | |
| [3.6](./3.6-scaling-laws-and-emergence.md) | Emergent Capabilities & Scaling Laws | 2–3 hours | |

---

## Prerequisites for This Phase

- All of [Phase 1 — ML Foundations](../phase-1-ml-foundations/README.md)
- All of [Phase 2 — Deep Learning](../phase-2-deep-learning/README.md) — especially Sections 2.3 and 2.4

---

## What You'll Be Able to Do After This Phase

- Explain how GPT, Claude, and Gemini are trained — including the full post-training pipeline
- Diagnose tokenization bugs that cause models to fail on simple tasks (counting letters, arithmetic)
- Explain why KV-cache memory grows linearly with context and what to do about it
- Tell the difference between factuality and faithfulness hallucinations and apply the right mitigation
- Read and understand LLM technical reports (model cards, training writeups)
- Reason about model capabilities based on scale, training data, and alignment approach

---

## The Arc of This Phase

```
3.1 Pre-training     → the raw capability: next-token prediction at planetary scale
3.2 Alignment        → shaping raw capability into useful, safe assistant behavior
3.3 Tokenization     → the often-overlooked layer between text and model
3.4 Context/KV-cache → the memory architecture that governs what the model can "see"
3.5 Hallucinations   → the structural failure mode you'll fight in every production system
3.6 Scaling laws     → why bigger works, and what "emergence" actually means
```

---

## Phase Navigation

| | |
|---|---|
| Previous Phase | [Phase 2 — Deep Learning](../phase-2-deep-learning/README.md) |
| Next Phase | Phase 4 — Prompt Engineering *(coming soon)* |
| Back to Roadmap | [Main README](../README.md) |

---

*Last updated: June 2026*
