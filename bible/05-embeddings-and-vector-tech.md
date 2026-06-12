# Chapter 5 — Embeddings & Vector Technology

> Every embedding model, vector database, and similarity search algorithm.

---

## 5.1 Embedding Models

### Commercial Embedding APIs

| Model | Provider | Dims | Context | Price ($/1M) | Type | Notes |
|---|---|---|---|---|---|---|
| **voyage-3-large** | Voyage AI | 1024 | 32K | $0.060 | Asymmetric | Best retrieval quality overall |
| **voyage-3** | Voyage AI | 1024 | 32K | $0.060 | Asymmetric | General purpose |
| **voyage-3-lite** | Voyage AI | 512 | 32K | $0.020 | Asymmetric | Budget option |
| **voyage-code-3** | Voyage AI | 1024 | 32K | $0.060 | Asymmetric | Code retrieval |
| **voyage-finance-2** | Voyage AI | 1024 | 32K | $0.120 | Asymmetric | Financial text |
| **voyage-law-2** | Voyage AI | 1024 | 32K | $0.120 | Asymmetric | Legal documents |
| **voyage-multilingual-2** | Voyage AI | 1024 | 32K | $0.060 | Asymmetric | 40+ languages |
| **text-embedding-3-small** | OpenAI | 1536 | 8K | $0.020 | Symmetric | Default; Matryoshka |
| **text-embedding-3-large** | OpenAI | 3072 | 8K | $0.130 | Symmetric | Best OpenAI; Matryoshka |
| **embed-v4.0** | Cohere | 1024 | 512 | $0.010 | Asymmetric | Cheapest commercial |
| **text-embedding-004** | Google | 768 | 2K | $0.025 | Symmetric | Good multilingual |
| **mistral-embed** | Mistral | 1024 | 8K | $0.100 | Symmetric | EU data residency |

**Asymmetric models** (Voyage, Cohere): specify `input_type="query"` or `input_type="document"` — different processing for each. Always required for best retrieval.

**Matryoshka embeddings** (OpenAI text-embedding-3): Truncate to any dimension with graceful quality degradation (3072 → 256 with ~5% loss).

---

### Open-Source / Self-Hosted Embedding Models

| Model | Dims | Context | Size | Notes |
|---|---|---|---|---|
| **bge-large-en-v1.5** | 1024 | 512 | 670MB | Best open English |
| **bge-m3** | 1024 | 8192 | 2.3GB | Best open multilingual (100+ langs) |
| **bge-reranker-large** | — | 512 | 1.3GB | Cross-encoder reranker |
| **all-MiniLM-L6-v2** | 384 | 256 | 80MB | Fast; good for prototyping |
| **all-mpnet-base-v2** | 768 | 384 | 420MB | Better quality than MiniLM |
| **e5-large-v2** | 1024 | 512 | 1.3GB | Strong retrieval |
| **e5-mistral-7b-instruct** | 4096 | 32K | 14GB | Highest quality open; needs GPU |
| **nomic-embed-text-v1.5** | 768 | 8192 | 300MB | Open; commercial-competitive |
| **GTE-Qwen2-7B** | 3584 | 32K | 15GB | Recent high-quality open |
| **BAAI/bge-en-icl** | 4096 | 512 | 7GB | In-context learning embedding |
| **stella_en_1.5B_v5** | 1024 | 512 | 3GB | Top MTEB open model 2025 |

**The MTEB Leaderboard** is the authoritative benchmark: [huggingface.co/spaces/mteb/leaderboard](https://huggingface.co/spaces/mteb/leaderboard)

---

### Reranking Models

Two-stage retrieval: bi-encoder retrieval (fast) → cross-encoder reranking (precise).

| Model | Provider | Notes |
|---|---|---|
| **rerank-v3.5** | Cohere | Best production reranker; API |
| **rerank-2** | Voyage AI | Strong quality; API |
| **jina-reranker-v2** | Jina AI | Free tier available |
| **bge-reranker-large** | BAAI | Open source; self-hosted |
| **ms-marco-MiniLM-L-6-v2** | HuggingFace | Fast; free; local |
| **cross-encoder/ms-marco-MiniLM-L-12-v2** | HuggingFace | Better quality version |

---

## 5.2 Vector Databases

### Feature Comparison Matrix

| Database | Type | Scale | Hybrid Search | Filtering | Self-Host | Best For |
|---|---|---|---|---|---|---|
| **Qdrant** | Purpose-built (Rust) | Billions | Yes (sparse+dense) | Excellent (payload) | Yes + Cloud | New projects; best price/perf |
| **Pinecone** | Managed cloud | Billions | Limited | Good | No | Zero-ops; enterprise SLAs |
| **Weaviate** | Purpose-built (Go) | Billions | Yes (native BM25) | Good | Yes + Cloud | Native hybrid search |
| **pgvector** | Postgres extension | ~50M | Manual (FTS+pgvector) | Full SQL | With Postgres | Already using Postgres |
| **Chroma** | Local/cloud | Millions | No | Basic | Yes | Development/prototyping |
| **Milvus** | Purpose-built | Billions | Yes | Good | Yes + Cloud | High-scale; complex queries |
| **Faiss** | Library (Meta) | Billions | No | No | Yes | Offline batch; custom pipelines |
| **Annoy** | Library (Spotify) | Millions | No | No | Yes | Read-heavy; can't add after build |
| **Redis Stack** | Redis module | Millions | Partial | Good | Yes + Cloud | Already using Redis; low latency |
| **Deep Lake** | LLM-specific | Millions | No | Good | Yes | Version-controlled data + vectors |
| **LanceDB** | Embedded (Rust) | Billions | Yes | Good | Yes | Serverless; no server needed |
| **Turbopuffer** | Serverless cloud | Billions | Yes | Good | No | Serverless; cheap at scale |

---

### Qdrant — Deep Dive

```
Architecture: Rust; HNSW index; segment-based storage
Filtering:     Indexed payload fields; smart pre/post-filter strategy
Sparse:        Native sparse vector support (SPLADE/BM25)
Collections:   Multiple collections; namespaces within
Distance:      Cosine, Dot Product, Euclidean, Manhattan
API:           REST + gRPC
```

**Key params:**
- `m`: HNSW graph connections (16 default; higher = better quality, more memory)
- `ef_construct`: Build-time beam width (100 default; higher = better, slower build)
- `ef`: Search-time beam width (per query; higher = better recall, slower)
- `on_disk`: Store vectors on disk (for very large collections)

---

### pgvector — Deep Dive

```sql
-- Install
CREATE EXTENSION vector;

-- Create table
CREATE TABLE documents (
  id bigserial PRIMARY KEY,
  content text,
  embedding vector(1536)
);

-- Create HNSW index (pgvector 0.5.0+)
CREATE INDEX ON documents
  USING hnsw (embedding vector_cosine_ops)
  WITH (m = 16, ef_construction = 64);

-- Create IVFFlat index (alternative)
CREATE INDEX ON documents
  USING ivfflat (embedding vector_cosine_ops)
  WITH (lists = 100);

-- Query
SELECT id, content, 1 - (embedding <=> '[0.1, ...]'::vector) AS score
FROM documents
ORDER BY embedding <=> '[0.1, ...]'::vector
LIMIT 5;
```

**Operators:**
- `<=>` Cosine distance
- `<#>` Negative dot product
- `<->` Euclidean distance
- `<+>` Taxicab distance (Manhattan)

**Ceiling:** ~50M vectors on a well-provisioned single Postgres instance.

---

### ANN Algorithms

| Algorithm | Memory | Build Time | Query Speed | Notes |
|---|---|---|---|---|
| **HNSW** | High | Slow | Fast | Default for most vector DBs |
| **IVFFlat** | Medium | Fast | Medium | Good for large datasets |
| **IVFPQ** | Low | Fast | Medium | Compressed vectors; billions scale |
| **NSG** | Medium | Medium | Faster than HNSW | Research; less ecosystem |
| **DiskANN** | Very low | Slow | Good | SSD-resident; Microsoft |
| **ScaNN** | Medium | Medium | Fastest at scale | Google; best high-dim |

---

## 5.3 Similarity Metrics

| Metric | Formula | When To Use |
|---|---|---|
| **Cosine similarity** | cos(a,b) = a·b / (‖a‖‖b‖) | Text embeddings; magnitude varies |
| **Dot product** | a·b | L2-normalized vectors (= cosine) |
| **Euclidean (L2)** | √Σ(aᵢ-bᵢ)² | When magnitude is meaningful |
| **Manhattan (L1)** | Σ|aᵢ-bᵢ| | Sparse features |
| **Hamming** | Count of differing bits | Binary/hash vectors |
| **Jaccard** | |A∩B| / |A∪B| | Set similarity |

**Rule:** Normalize embeddings to unit length. Then dot product = cosine similarity. Faster to compute.

---

## 5.4 Chunking Strategies

| Strategy | Split At | Quality | Cost | Best For |
|---|---|---|---|---|
| **Fixed character** | Every N chars | Poor | Lowest | Avoid |
| **Recursive character** | Paragraph → sentence → word | Good | Low | Default choice (80% of cases) |
| **Token-based** | Every N tokens | Good | Low | When token count matters |
| **Sentence** | Sentence boundary | Good | Low | Q&A, semantic search |
| **Semantic** | Embedding similarity breaks | Better | Medium | Multi-topic docs |
| **Markdown/HTML** | Header/section boundaries | Good | Low | Structured documents |
| **Parent-child** | Small for retrieval, large for context | Best | Medium | Complex docs |
| **Agentic** | LLM decides boundaries | Theoretically best | High | Emerging |

**Optimal chunk sizes (tokens):**
- General text: 256–512 tokens, 64-token overlap
- Technical docs: 512–1024 tokens
- Legal/financial: 1024–2048 tokens
- Code: 384–512 tokens (function/class boundaries)

---

*[← Chapter 4: Inference & Serving](./04-inference-and-serving.md) | [Chapter 6: RAG & Retrieval →](./06-rag-and-retrieval.md)*
