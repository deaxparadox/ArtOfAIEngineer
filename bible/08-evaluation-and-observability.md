# Chapter 8 — Evaluation & Observability

> Every eval framework, observability platform, testing tool, and monitoring approach.

---

## 8.1 Evaluation Frameworks

### RAGAS

The standard framework for RAG evaluation. LLM-as-judge.

| Metric | What It Measures |
|---|---|
| `context_recall` | Did retrieved chunks contain the needed info? |
| `context_precision` | Were retrieved chunks actually relevant? |
| `faithfulness` | Is the answer grounded in the retrieved context? |
| `answer_relevancy` | Does the answer address the question? |
| `context_entity_recall` | Were relevant entities retrieved? |
| `noise_sensitivity` | How much does irrelevant context hurt? |

**Install:** `pip install ragas`

---

### DeepEval

Most comprehensive open-source LLM eval framework. 30+ metrics.

| Category | Metrics |
|---|---|
| **RAG** | Faithfulness, answer relevancy, contextual recall/precision |
| **Conversation** | Coherence, role adherence, knowledge retention |
| **Agents** | Tool correctness, task completion |
| **Safety** | Bias, toxicity, PII leakage |
| **Custom** | G-Eval (rubric-based), any custom metric |

**Key feature:** `pytest`-compatible; easy CI/CD integration.

---

### TruLens (TruEra)

Open-source RAG evaluation with the TruLens Triad.

| Metric | Description |
|---|---|
| **Groundedness** | Is the response supported by the retrieved context? |
| **Context relevance** | Is the retrieved context relevant to the query? |
| **Answer relevance** | Is the final answer relevant to the query? |

---

### PromptFoo

CLI-first prompt testing and evaluation.

```yaml
# promptfoo.yaml
prompts:
  - "Answer this: {{question}}"
providers:
  - openai:gpt-4o
  - anthropic:claude-sonnet-4-6
tests:
  - vars:
      question: "What is the capital of France?"
    assert:
      - type: contains
        value: Paris
      - type: llm-rubric
        value: Answer is factually correct and concise
```

**Best for:** CLI-driven; easy CI integration; multi-provider comparison.

---

### Braintrust

Commercial eval platform with strong CI/CD integration.

| Feature | Detail |
|---|---|
| **Datasets** | Versioned eval datasets |
| **Experiments** | Compare across models, prompts, versions |
| **Scoring** | LLM-as-judge + custom scorers |
| **CI/CD** | GitHub Actions integration |
| **Replay** | Replay past experiments on new models |

---

### Giskard

Open-source AI quality and safety testing.

| Feature | Detail |
|---|---|
| **LLM scan** | Automatic vulnerability detection |
| **RAG evaluation** | Correctness, groundedness, pertinence |
| **Safety tests** | Prompt injection, hallucination detection |

---

### HELM (Stanford)

Holistic Evaluation of Language Models. Broad benchmark suite.

- 30+ scenarios
- 7 metrics per scenario
- Comparison across 100+ models
- [crfm.stanford.edu/helm](https://crfm.stanford.edu/helm)

---

## 8.2 LLM-as-Judge Methods

| Method | Description | Bias Mitigation |
|---|---|---|
| **Direct scoring** | Score 1–5 against a rubric | Position bias; verbosity bias |
| **Pairwise comparison** | A vs B; pick the better one | Run both orderings; cancel position bias |
| **Reference-based** | Compare to reference answer | Need ground truth |
| **G-Eval** | CoT before scoring; structured rubric | More reliable than direct scoring |
| **Calibrated judge** | Tuned against human labels | Highest reliability |
| **Ensemble judge** | Multiple judges; majority vote | Reduces individual bias |

**Known biases in LLM judges:**
- Verbosity bias (prefers longer)
- Position bias (prefers first in pairwise)
- Self-preference (model prefers own style)
- Sycophancy (agrees with authoritative tone)
- Language bias (penalizes non-English)

---

## 8.3 Observability Platforms

### Langfuse

**Type:** Open source + cloud. Most popular open observability for LLMs.

| Feature | Detail |
|---|---|
| **Tracing** | Full request traces with spans |
| **Prompt management** | Version and deploy prompts |
| **Eval integration** | Custom scorers; LLM-as-judge |
| **Cost tracking** | Per-model, per-user |
| **Self-hostable** | Postgres + ClickHouse |
| **SDK** | Python, JS/TS, Go |

**Setup:** `pip install langfuse` + 2 env vars.

---

### LangSmith (LangChain)

**Type:** Commercial. Deep integration with LangChain/LangGraph.

| Feature | Detail |
|---|---|
| **Deep tracing** | Node-by-node state diffs in LangGraph |
| **Datasets** | Versioned eval datasets |
| **Evals** | Built-in + custom |
| **Prompt hub** | Shared prompt library |
| **Annotation** | Human feedback collection |

**Best for:** LangChain/LangGraph-heavy stacks.

---

### Helicone

**Type:** Commercial (proxy-based). Simplest setup.

| Feature | Detail |
|---|---|
| **Setup** | Change one `base_url`; done |
| **Cost tracking** | Per-request costs |
| **Caching** | Semantic cache |
| **Rate limiting** | Per-user/team limits |
| **Depth** | API-call level (not agent step level) |

**Best for:** Teams wanting zero-code observability setup.

---

### Arize Phoenix

**Type:** Open source + cloud. ML monitoring heritage.

| Feature | Detail |
|---|---|
| **Traces** | Full OTEL-compatible tracing |
| **Evals** | LLM-as-judge; RAG-specific |
| **Drift** | Input/output distribution monitoring |
| **Embeddings** | Embedding drift visualization |

**Best for:** Teams with existing ML monitoring; drift detection.

---

### Portkey

**Type:** Commercial gateway + observability.

| Feature | Detail |
|---|---|
| **Gateway** | Unified API across 250+ models |
| **Caching** | Semantic + exact caching |
| **Retry** | Automatic retry with fallback |
| **Observability** | Traces, costs, latency |

---

### Other Platforms

| Platform | Type | Notes |
|---|---|---|
| **Datadog LLM Obs** | Commercial APM | For existing Datadog users |
| **Honeycomb LLM** | Commercial | Deep event-based tracing |
| **New Relic AI** | Commercial APM | Broad coverage |
| **MLflow (v3.0+)** | Open source | GenAI tracing; unified with ML |
| **W&B Prompts** | Commercial | Weights & Biases ecosystem |
| **Traceloop** | Open source | OpenTelemetry-based |

---

## 8.4 What to Observe

### Minimum Production Observability

Every LLM production system should capture:

```
Per Request:
  ✓ request_id          (trace correlation)
  ✓ user_id             (anonymized)
  ✓ feature_name        (which product feature)
  ✓ model               (exact model ID used)
  ✓ input_tokens        (from response.usage)
  ✓ output_tokens       (from response.usage)
  ✓ cost_usd            (computed)
  ✓ latency_ms          (TTFT + total)
  ✓ stop_reason         (end_turn vs max_tokens)
  ✓ is_error            (bool)
  ✓ environment         (prod/staging/dev)
```

### For RAG Systems Add

```
  ✓ retrieval_latency_ms
  ✓ n_chunks_retrieved
  ✓ top_chunk_score
  ✓ context_tokens
  ✓ citations_found (bool)
```

### For Agent Systems Add

```
  ✓ n_iterations
  ✓ tools_called (list)
  ✓ total_agent_cost_usd
  ✓ completion_status (completed/timeout/error)
```

---

## 8.5 Alerting Thresholds (Reference)

| Alert | Threshold | Severity |
|---|---|---|
| Error rate spike | > 2% | HIGH |
| Quality score drop | > 0.2 points (rolling 1h) | HIGH |
| Cost spike | > 3× baseline hourly | CRITICAL |
| P95 latency spike | > 2× baseline | MEDIUM |
| KV-cache memory | > 92% utilization | HIGH |
| Agent loop detected | Same tool called 3× | HIGH |
| PII in output | Any detection | CRITICAL |

---

*[← Chapter 7: Agents & Orchestration](./07-agents-and-orchestration.md) | [Chapter 9: MLOps & Platforms →](./09-mlops-and-platforms.md)*
