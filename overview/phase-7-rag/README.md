# Phase 7 — RAG (Retrieval-Augmented Generation)

> **The most important pattern in production AI engineering.** RAG is how you give LLMs access
> to your private, current, and domain-specific knowledge — without fine-tuning, without
> retraining, and without paying to put your entire knowledge base in context every request.

---

## Why This Phase Matters

RAG is not a novelty. It's the architecture that makes LLMs useful for real business problems:

- **"Our model doesn't know about our products."** → RAG solves this.
- **"The model answers based on outdated information."** → RAG solves this.
- **"We can't send customer data to the LLM."** → RAG solves this (retrieve, don't embed all data).
- **"The model hallucinates facts."** → Grounded RAG reduces this significantly.

80% of enterprise software developers now cite RAG as the most effective way to ground LLMs
in factual data. Understanding how to build it correctly — not just naively — is a core
production AI engineering skill.

---

## Sections

| # | Topic | Time Estimate | Status |
|---|---|---|---|
| [7.1](./7.1-rag-fundamentals.md) | RAG Fundamentals: Why It Exists & What It Solves | 2–3 hours | |
| [7.2](./7.2-naive-rag.md) | Naive RAG: The Basic Pipeline | 3–4 hours | |
| [7.3](./7.3-advanced-rag.md) | Advanced RAG: Reranking, Query Expansion & HyDE | 4–5 hours | |
| [7.4](./7.4-agentic-rag.md) | Agentic RAG: When Retrieval Is a Tool, Not a Step | 3–4 hours | |
| [7.5](./7.5-rag-evaluation.md) | Evaluation: How to Know If Your RAG Actually Works | 3–4 hours | |
| [7.6](./7.6-rag-failure-modes.md) | Common RAG Failure Modes & How to Fix Them | 3–4 hours | |

---

## Prerequisites for This Phase

- All of [Phase 6 — Embeddings & Semantic Search](../phase-6-embeddings-semantic-search/README.md)
- [Phase 4 — Prompt Engineering](../phase-4-prompt-engineering/README.md)
- [Phase 5 — Building with LLM APIs](../phase-5-building-with-llm-apis/README.md)

---

## What You'll Be Able to Do After This Phase

- Build a complete RAG pipeline from document ingestion to grounded LLM response
- Improve retrieval quality with reranking, query expansion, and HyDE
- Design an agentic RAG system that decides what and when to retrieve
- Measure RAG quality objectively with RAGAS and custom eval metrics
- Diagnose the 10 most common RAG failure modes and apply targeted fixes

---

## The Progression

```
7.1 Fundamentals      → why RAG, when to use it, the core problem it solves
7.2 Naive RAG         → the minimum viable pipeline that actually works
7.3 Advanced RAG      → techniques that close the gap between demo and production
7.4 Agentic RAG       → the next evolution: dynamic, multi-step retrieval
7.5 Evaluation        → measuring quality objectively (most teams skip this)
7.6 Failure modes     → a field guide to what breaks and why
```

---

## Phase Navigation

| | |
|---|---|
| Previous Phase | [Phase 6 — Embeddings & Semantic Search](../phase-6-embeddings-semantic-search/README.md) |
| Next Phase | Phase 8 — Tool Use & AI Agents *(coming soon)* |
| Back to Roadmap | [Main README](../README.md) |

---

*Last updated: June 2026*
