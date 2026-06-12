# Phase 12 — Deployment & Infrastructure

> **The final mile.** You've built a great AI system. Now make it serve real users at real scale,
> reliably and economically. This phase covers the engineering that turns a working model into a
> production serving system.

---

## Why This Phase Matters

Most AI engineers understand how models work. Fewer understand how to serve them efficiently.
The gap matters enormously at scale:

- Serving a 70B model naively costs 10× more and is 10× slower than serving it correctly
- A single GPU can serve 100 concurrent users with the right batching, or 5 without it
- Quantization can halve memory requirements with <1% quality loss — or degrade quality catastrophically
- The difference between good and great LLM infrastructure is often a factor of 5–10× in cost

This phase teaches the engineering primitives that production ML serving is built on.

---

## Sections

| # | Topic | Time Estimate | Status |
|---|---|---|---|
| [12.1](./12.1-model-serving-frameworks.md) | Model Serving: vLLM, TorchServe & Triton | 3–4 hours | |
| [12.2](./12.2-gpu-memory-batching-throughput.md) | GPU Memory Management, Batching & Throughput | 4–5 hours | |
| [12.3](./12.3-quantization.md) | Quantization: INT8, INT4, GPTQ, AWQ | 3–4 hours | |
| [12.4](./12.4-distributed-inference.md) | Distributed Inference & Tensor Parallelism | 3–4 hours | |
| [12.5](./12.5-latency-vs-throughput.md) | Latency vs Throughput Tradeoffs | 3–4 hours | |
| [12.6](./12.6-cost-optimization.md) | Cost Optimization: Caching, Batching & Model Selection | 3–4 hours | |

---

## Prerequisites for This Phase

- [Phase 11 — Fine-Tuning](../phase-11-fine-tuning/README.md)
- [3.4 — Context Windows & KV-Cache](../phase-3-large-language-models/3.4-context-windows-kv-cache.md) — KV-cache mechanics
- Basic Docker/Kubernetes concepts
- Familiarity with GPU concepts (VRAM, compute vs memory-bound)

---

## What You'll Be Able to Do After This Phase

- Deploy a self-hosted LLM with vLLM and serve it via an OpenAI-compatible API
- Configure continuous batching and PagedAttention for maximum throughput
- Quantize a model to INT4/INT8 with GPTQ or AWQ and measure quality tradeoff
- Set up multi-GPU tensor parallelism for large models
- Make the right latency vs throughput decision for your use case
- Implement speculative decoding, prompt caching, and model routing for cost reduction

---

## The Serving Problem in One Number

A naive LLM serving setup might handle **5 requests/second** on an A100.
A production-optimized setup with continuous batching, PagedAttention, and the right
quantization can handle **50–100+ requests/second** on the same hardware.

That's a 10–20× efficiency difference from infrastructure engineering alone.

---

## Phase Navigation

| | |
|---|---|
| Previous Phase | [Phase 11 — Fine-Tuning](../phase-11-fine-tuning/README.md) |
| Next Phase | *Roadmap complete* |
| Back to Roadmap | [Main README](../README.md) |

---

*Last updated: June 2026*
