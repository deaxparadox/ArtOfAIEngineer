# The AI Engineering Bible

> A comprehensive reference for every concept, technology, tool, model, and framework in the AI engineering ecosystem — as of June 2026.
>
> This is not a learning path. It is a **reference manual** — the single document you return to when you need to know what something is, how it works, when to use it, and how it compares to alternatives.

---

## How to Use This Bible

- **Exploring a new topic?** Start with the chapter index below, pick a chapter, read end-to-end.
- **Looking up something specific?** Use your editor's search (`Ctrl+F` / `Cmd+F`) within any chapter.
- **Comparing options?** Every chapter contains comparison tables.
- **Staying current?** All entries are dated June 2026. The field moves fast — verify pricing and specs at source.

---

## Chapters

| # | Chapter | What It Covers |
|---|---|---|
| [1](./01-foundation-models-and-providers.md) | Foundation Models & Providers | Every major LLM: specs, pricing, context, strengths |
| [2](./02-architectures-and-algorithms.md) | Architectures & Algorithms | Transformers, CNNs, RNNs, SSMs, MoE — every major architecture |
| [3](./03-training-techniques.md) | Training Techniques | Pre-training, SFT, RLHF, DPO, RLVR, LoRA, QLoRA — all methods |
| [4](./04-inference-and-serving.md) | Inference & Serving | vLLM, Triton, TorchServe, quantization, deployment patterns |
| [5](./05-embeddings-and-vector-tech.md) | Embeddings & Vector Technology | Every embedding model and vector database |
| [6](./06-rag-and-retrieval.md) | RAG & Retrieval | Chunking, hybrid search, advanced RAG, evaluation metrics |
| [7](./07-agents-and-orchestration.md) | Agents & Orchestration | All agent frameworks, patterns, MCP, tool use |
| [8](./08-evaluation-and-observability.md) | Evaluation & Observability | Every eval framework, observability platform, testing tool |
| [9](./09-mlops-and-platforms.md) | MLOps & Platforms | Experiment tracking, model registries, CI/CD, feature stores |
| [10](./10-hardware-and-cloud.md) | Hardware & Cloud | GPUs, TPUs, cloud AI services, cost comparison |
| [11](./11-security-and-safety.md) | Security & Safety | Alignment, guardrails, red-teaming, OWASP LLM Top 10 |
| [12](./12-key-papers-and-benchmarks.md) | Key Papers & Benchmarks | Canon papers every AI engineer should know; all major benchmarks |
| [13](./13-complete-tool-catalog.md) | Complete Tool Catalog | Every tool, library, and platform — categorized and cross-referenced |

---

## At a Glance: The 2026 AI Engineering Stack

```
┌─────────────────────────────────────────────────────────────────────┐
│  FOUNDATION MODELS                                                  │
│  Anthropic · OpenAI · Google · Meta · Mistral · DeepSeek · Qwen   │
├─────────────────────────────────────────────────────────────────────┤
│  ORCHESTRATION & AGENTS                                             │
│  LangChain · LlamaIndex · LangGraph · CrewAI · AutoGen · MCP      │
├─────────────────────────────────────────────────────────────────────┤
│  RETRIEVAL (RAG)                                                    │
│  Embeddings: Voyage · OpenAI · Cohere · BGE                        │
│  Vector DBs: Qdrant · Pinecone · Weaviate · pgvector               │
├─────────────────────────────────────────────────────────────────────┤
│  INFERENCE & SERVING                                                │
│  vLLM · SGLang · Triton · TensorRT-LLM · Ollama                   │
├─────────────────────────────────────────────────────────────────────┤
│  EVALUATION & OBSERVABILITY                                         │
│  RAGAS · DeepEval · Langfuse · LangSmith · Helicone · Braintrust  │
├─────────────────────────────────────────────────────────────────────┤
│  MLOPS & TRAINING                                                   │
│  MLflow · W&B · DVC · Hugging Face · Axolotl · TRL                │
├─────────────────────────────────────────────────────────────────────┤
│  HARDWARE & CLOUD                                                   │
│  NVIDIA H200 · AWS · GCP · Azure · RunPod · Lambda Labs           │
└─────────────────────────────────────────────────────────────────────┘
```

---

## Quick Reference: Most Important Decisions in AI Engineering

| Decision | Chapter | Short Answer |
|---|---|---|
| Which LLM for production? | [Ch. 1](./01-foundation-models-and-providers.md) | Claude Sonnet for quality, gpt-4o-mini for cost, Llama 4 for self-hosting |
| Which vector DB? | [Ch. 5](./05-embeddings-and-vector-tech.md) | Qdrant (new projects), pgvector (already on Postgres) |
| Which embedding model? | [Ch. 5](./05-embeddings-and-vector-tech.md) | Voyage-3-large (best), text-embedding-3-small (default OpenAI) |
| When to fine-tune vs RAG? | [Ch. 3](./03-training-techniques.md) | RAG for knowledge, fine-tune for behavior/format |
| Which agent framework? | [Ch. 7](./07-agents-and-orchestration.md) | LangGraph (production), CrewAI (role-based) |
| Which serving framework? | [Ch. 4](./04-inference-and-serving.md) | vLLM (single LLM), Triton (multi-model) |
| Which eval tool? | [Ch. 8](./08-evaluation-and-observability.md) | RAGAS (RAG), DeepEval (general), Langfuse (observability) |
| How to quantize? | [Ch. 4](./04-inference-and-serving.md) | AWQ INT4 for memory-constrained, FP8 for H100 |

---

*Sources: Research conducted June 2026. Prices and specs change frequently — verify at provider dashboards.*
*For a structured learning path through these concepts: [AI Engineer Roadmap →](../overview/README.md)*
