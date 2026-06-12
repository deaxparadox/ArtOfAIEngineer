# Chapter 6 — RAG & Retrieval

> Every retrieval pattern, pipeline stage, optimization technique, and evaluation metric.

---

## 6.1 RAG Pipeline Taxonomy

### Naive RAG
Minimal viable RAG: embed query → ANN search → inject top-K chunks → generate.

```
Query → Embed → Vector Search → Top-K chunks → LLM → Answer
```

**Failure rate:** ~73% of failures are retrieval failures (wrong chunks retrieved), not generation failures.

---

### Advanced RAG Techniques

#### Pre-Retrieval (Query Transformation)

| Technique | What It Does | Latency Cost | Quality Gain |
|---|---|---|---|
| **Query expansion** | Generate N alternative phrasings | +100–300ms | +10–18% recall |
| **HyDE** | Generate hypothetical answer; embed that | +100–200ms | +5–12% recall |
| **Step-back prompting** | Abstract to general principle first | +100ms | +5–10% reasoning |
| **Multi-query retrieval** | Run N queries, merge results | +200–400ms | +10–18% recall |
| **Query routing** | Send to the right knowledge base | +50ms | Depends |
| **Sub-query decomposition** | Break complex query into parts | +200ms | +15–25% complex Q |

#### Post-Retrieval (Result Enhancement)

| Technique | What It Does | Latency Cost | Quality Gain |
|---|---|---|---|
| **Reranking** | Cross-encoder re-scores top-20 | +50–200ms | +8–15% precision |
| **Contextual compression** | LLM extracts relevant sentences | +50–150ms | Reduces context noise |
| **Lost-in-middle mitigation** | Place relevant chunks at start/end | None | +5–10% faithfulness |
| **Fusion** | Merge results from multiple retrievers | Minimal | +10–20% recall |
| **Citation extraction** | Extract source references from response | +50ms | Auditing |

---

### Agentic RAG

Retrieval becomes a tool the agent calls dynamically, not a fixed pipeline step.

| Pattern | Description | When to Use |
|---|---|---|
| **ReAct + search tool** | Agent decides when to search | Multi-hop Q&A |
| **Self-ask** | Agent generates sub-questions | Complex analysis |
| **Plan-and-execute** | Plan all retrievals, execute | Structured tasks |
| **Graph RAG** | Traverse knowledge graphs | Relational knowledge |
| **Multi-hop RAG** | Sequential retrievals building on prior | Reasoning chains |
| **Adaptive RAG** | Router decides naive vs agentic path | Mixed workloads |

---

## 6.2 Hybrid Search

Combining dense vector search with sparse keyword search.

### BM25 (Sparse Retrieval)

```
BM25(q, d) = Σᵢ IDF(tᵢ) × TF(tᵢ, d) × (k₁+1) / (TF + k₁(1-b+b|d|/avgdl))
```

- Fast (inverted index lookup; no GPU)
- Exact keyword matching
- Fails on semantics; excels on technical identifiers

### Score Fusion Methods

| Method | Formula | Tuning Needed | Notes |
|---|---|---|---|
| **RRF** (Reciprocal Rank Fusion) | score = Σ 1/(k+rank) | No (k=60) | Default; robust |
| **Weighted** | score = α × dense + (1-α) × sparse | Yes (α via labels) | +5–10% over RRF with tuning |
| **Dynamic α** | α adjusted per query type | Yes | Frontier 2025–2026 |
| **CombSUM** | Normalize then sum | Yes | Simple |

### BM25 Implementations

| Library | Language | Notes |
|---|---|---|
| **rank-bm25** | Python | Simple; pure Python |
| **bm25s** | Python (Cython) | 10–100× faster than rank-bm25 |
| **elasticsearch/opensearch** | Any | Production-grade; managed |
| **tantivy** | Python (Rust) | Fast; used by LlamaIndex |
| **whoosh** | Python | Pure Python; smaller scale |

---

## 6.3 RAG Evaluation Metrics (RAGAS)

The four key metrics from the [RAGAS framework](https://github.com/explodinggradients/ragas):

| Metric | Measures | How Computed | Target |
|---|---|---|---|
| **Context Recall** | Was the needed information retrieved? | Check if ground truth claims appear in chunks | > 0.80 |
| **Context Precision** | Are retrieved chunks relevant? | What fraction of chunks actually matter? | > 0.75 |
| **Answer Faithfulness** | Is the answer grounded in context? | Extract claims; verify each against chunks | > 0.90 |
| **Answer Relevancy** | Does the answer address the question? | Semantic similarity to original question | > 0.85 |

**Additional metrics:**

| Metric | From | Measures |
|---|---|---|
| **Retrieval Recall@K** | Custom | Are relevant docs in top-K? |
| **MRR** (Mean Reciprocal Rank) | Custom | Rank of first relevant result |
| **nDCG** | Information retrieval | Ranking quality |
| **Groundedness** | Azure AI | Faithfulness variant |

---

## 6.4 RAG Failure Mode Taxonomy

| Failure Mode | Root Cause | Fix |
|---|---|---|
| **Semantic gap** | Query/doc vocabulary mismatch | Hybrid search; query expansion |
| **Chunk boundary** | Answer splits across chunks | More overlap; parent-child retrieval |
| **Identifier miss** | Exact code/name not retrieved | Hybrid search; metadata filtering |
| **Stale knowledge** | Knowledge base not updated | Re-indexing pipeline |
| **Multi-document** | Answer requires N docs | Agentic RAG; self-ask |
| **Context ignored** | LLM overrides retrieved context | Stronger grounding prompt |
| **Hallucination** | LLM adds info beyond context | Citation forcing; claim verification |
| **Contradictions** | Multiple document versions | Version metadata; dedup |
| **Lost in middle** | Long context; relevant chunk ignored | Rank-first context ordering |
| **Multi-turn drift** | Conversation history crowds out context | Re-retrieve each turn |

---

## 6.5 Document Processing Pipeline

```
Raw document (PDF/HTML/DOCX/etc.)
        ↓ Parsing
Extracted text (structure-aware: headers, tables, code)
        ↓ Cleaning
Cleaned text (remove boilerplate, fix encoding, normalize)
        ↓ Chunking
Chunks (with metadata: source, page, section, timestamp)
        ↓ Embedding
Vectors (1024–3072 dimensional float arrays)
        ↓ Indexing
Vector DB + metadata store
```

### Document Parsers

| Tool | Best For | Notes |
|---|---|---|
| **pypdf / PyPDF2** | Digital PDFs | Fast; fails on scanned |
| **pdfplumber** | PDFs with tables | Better table extraction |
| **pymupdf (fitz)** | PDFs; layout-aware | Best general PDF parser |
| **docling** (IBM) | Enterprise docs | Multi-format; layout detection |
| **unstructured.io** | Multi-format | PDF, DOCX, HTML, email |
| **markitdown** (Microsoft) | Convert any doc to Markdown | Good for LLM ingestion |
| **llmsherpa** | Hierarchical PDF structure | Preserves headings |
| **camelot** | Tables in PDFs | Table extraction specialist |

---

*[← Chapter 5: Embeddings & Vector Tech](./05-embeddings-and-vector-tech.md) | [Chapter 7: Agents & Orchestration →](./07-agents-and-orchestration.md)*
