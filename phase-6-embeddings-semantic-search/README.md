# Phase 6 — Embeddings & Semantic Search

> **The retrieval layer.** RAG, semantic search, recommendation systems, duplicate detection,
> clustering — all of these are built on one foundational idea: representing meaning as vectors
> and finding similar vectors efficiently. This phase gives you that foundation.

---

## Why This Phase Matters

Embeddings are the invisible glue in modern AI systems:
- **RAG** works because relevant documents have vectors close to the query vector
- **Semantic search** works because "car" and "automobile" have similar embeddings
- **Recommendation engines** work because users who liked similar items cluster in embedding space
- **Duplicate detection** works because near-identical content has near-identical vectors

Understanding this layer is what separates engineers who can build retrieval systems from engineers
who can only wire together pre-built ones. When retrieval quality is poor — and it often is —
you need to know *which lever to pull*: model choice, chunking, similarity metric, or hybrid strategy.

---

## Sections

| # | Topic | Time Estimate | Status |
|---|---|---|---|
| [6.1](./6.1-what-are-embeddings.md) | What Are Embeddings? From Tokens to Vectors | 2–3 hours | |
| [6.2](./6.2-embedding-models.md) | Embedding Models: Choosing & Comparing | 3–4 hours | |
| [6.3](./6.3-similarity-search.md) | Similarity Search: Cosine, Dot Product & ANN | 3–4 hours | |
| [6.4](./6.4-vector-databases.md) | Vector Databases: Pinecone, Weaviate, Qdrant, pgvector | 3–4 hours | |
| [6.5](./6.5-chunking-strategies.md) | Chunking Strategies That Actually Work | 3–4 hours | |
| [6.6](./6.6-hybrid-search.md) | Hybrid Search: Dense + Sparse (BM25) | 3–4 hours | |

---

## Prerequisites for This Phase

- [Phase 5 — Building with LLM APIs](../phase-5-building-with-llm-apis/README.md)
- [2.4 — The Transformer Architecture](../phase-2-deep-learning/2.4-transformer-architecture.md) — encoder models
- Basic Python + NumPy

---

## What You'll Be Able to Do After This Phase

- Explain what an embedding is and why similar content has similar vectors
- Choose the right embedding model for English, multilingual, and domain-specific text
- Compute and compare cosine similarity; understand when to use ANN vs exact search
- Set up a vector database (Qdrant or pgvector) and perform semantic search
- Design chunking strategies that maximize retrieval precision for your document type
- Build hybrid search that combines dense + sparse retrieval for higher recall

---

## The Arc of This Phase

```
6.1 What are embeddings?     → the concept: meaning as coordinates in space
6.2 Embedding models         → which models produce the best vectors for your use case
6.3 Similarity search        → how to find close vectors efficiently at scale
6.4 Vector databases         → where to store and query millions of vectors
6.5 Chunking                 → how to split documents so retrieval actually works
6.6 Hybrid search            → combining dense + sparse for production-grade retrieval
```

---

## Phase Navigation

| | |
|---|---|
| Previous Phase | [Phase 5 — Building with LLM APIs](../phase-5-building-with-llm-apis/README.md) |
| Next Phase | Phase 7 — RAG *(coming soon)* |
| Back to Roadmap | [Main README](../README.md) |

---

*Last updated: June 2026*
