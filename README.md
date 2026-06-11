# The Art of AI Engineering — Roadmap

> A practitioner's guide to becoming a production AI engineer. Not a blog post. Not a marketing page.
> Built from real engineering experience: training models, shipping RAG pipelines, debugging hallucinations at 3am,
> and watching providers deprecate APIs you built critical features on.

---

## Who This Is For

- Software engineers who want to move into AI engineering
- Data scientists who want to build production-grade AI systems (not just notebooks)
- Anyone who can already code in Python and wants a structured path into the LLM ecosystem

**Not for:** people looking for a "no-code AI" path. This is an engineering roadmap.

---

## How to Use This Roadmap

Each phase builds on the previous. **Don't skip Phase 1–3 even if you "know ML"** — the concepts map directly to how LLMs behave in ways that will save you hours of debugging later.

You can jump to any topic, but if something isn't clicking, go back to its prerequisites.

**Estimated time:** 6–12 months for someone coding daily. Not a weekend course.

---

## The Roadmap

| Phase | Topic | Status |
|---|---|---|
| [Phase 1](./phase-1-ml-foundations/README.md) | ML Foundations | ✅ Complete |
| [Phase 2](./phase-2-deep-learning/README.md) | Deep Learning | ✅ Complete |
| [Phase 3](./phase-3-large-language-models/README.md) | Large Language Models | ✅ Complete |
| [Phase 4](./phase-4-prompt-engineering/README.md) | Prompt Engineering | ✅ Complete |
| [Phase 5](./phase-5-building-with-llm-apis/README.md) | Building with LLM APIs | ✅ Complete |
| [Phase 6](./phase-6-embeddings-semantic-search/README.md) | Embeddings & Semantic Search | ✅ Complete |
| [Phase 7](./phase-7-rag/README.md) | RAG (Retrieval-Augmented Generation) | ✅ Complete |
| [Phase 8](./phase-8-tool-use-agents/README.md) | Tool Use & AI Agents | ✅ Complete |
| [Phase 9](./phase-9-evals-quality/README.md) | Evals & Quality | ✅ Complete |
| [Phase 10](./phase-10-mlops-production/README.md) | MLOps & Production AI | ✅ Complete |
| [Phase 11](./phase-11-fine-tuning/README.md) | Fine-Tuning | ✅ Complete |
| [Phase 12](./phase-12-deployment-infrastructure/README.md) | Deployment & Infrastructure | ✅ Complete |

---

## Phase 1 — ML Foundations

> What you need to understand before any of this makes sense.
>
> → **[Full Phase 1 content with all sections](./phase-1-ml-foundations/README.md)**

| Topic | What You'll Learn |
|---|---|
| [1.1 What is machine learning?](./phase-1-ml-foundations/1.1-what-is-machine-learning.md) | Types and taxonomy: supervised, unsupervised, reinforcement |
| [1.2 How neural networks learn](./phase-1-ml-foundations/1.2-how-neural-networks-learn.md) | Forward pass, loss functions, backpropagation |
| [1.3 Gradient descent & optimizers](./phase-1-ml-foundations/1.3-gradient-descent-and-optimizers.md) | SGD, Adam, AdamW — why they exist and when they fail |
| [1.4 Overfitting & evaluation](./phase-1-ml-foundations/1.4-overfitting-regularization-evaluation.md) | Regularization, train/val/test splits, precision/recall/F1 |
| [1.5 ML → Deep Learning](./phase-1-ml-foundations/1.5-path-to-deep-learning.md) | How scale and data changed what's possible |

**Key insight:** You don't need to implement backprop from scratch. You need to understand it well enough to know *why* your training loss is behaving the way it is.

**Resources:**
- [fast.ai Practical Deep Learning](https://course.fast.ai) — bottom-up, code-first
- [3Blue1Brown Neural Networks playlist](https://www.youtube.com/playlist?list=PLZHQObOWTQDNU6R1_67000Dx_ZCJB-3pi) — best visual intuition available
- [StatQuest with Josh Starmer](https://www.youtube.com/@statquest) — for the stats underpinning

---

## Phase 2 — Deep Learning

> The architectural building blocks that everything else is built on.
>
> → **[Full Phase 2 content with all sections](./phase-2-deep-learning/README.md)**

| Topic | What You'll Learn |
|---|---|
| [2.1 CNNs](./phase-2-deep-learning/2.1-cnns-convolutional-neural-networks.md) | Convolutional layers, pooling, residual connections, image understanding |
| [2.2 RNNs & LSTMs](./phase-2-deep-learning/2.2-rnns-and-lstms.md) | Sequential data, memory gates, vanishing gradients, when LSTMs still matter |
| [2.3 Attention Mechanism](./phase-2-deep-learning/2.3-attention-mechanism.md) | Q/K/V, scaled dot-product, multi-head, causal masking |
| [2.4 Transformer Architecture](./phase-2-deep-learning/2.4-transformer-architecture.md) | Full architecture deep dive, encoder vs decoder, FFN as memory, positional encoding |
| [2.5 Transfer Learning](./phase-2-deep-learning/2.5-transfer-learning-and-fine-tuning.md) | Pre-trained models, fine-tuning strategies, when to fine-tune vs prompt |

**Key insight:** Read the original "Attention Is All You Need" paper (Vaswani et al., 2017). Not because you'll implement it, but because understanding *why* transformers replaced RNNs tells you exactly what LLMs are good and bad at.

**Resources:**
- [The Illustrated Transformer — Jay Alammar](https://jalammar.github.io/illustrated-transformer/)
- [Andrej Karpathy: Let's build GPT from scratch](https://www.youtube.com/watch?v=kCc8FmEb1nY) — the single best resource for understanding transformers
- [PyTorch documentation](https://pytorch.org/docs/stable/index.html)

---

## Phase 3 — Large Language Models

> How LLMs are built, what they actually are, and why they behave the way they do.
>
> → **[Full Phase 3 content with all sections](./phase-3-large-language-models/README.md)**

| Topic | What You'll Learn |
|---|---|
| [3.1 Pre-training at scale](./phase-3-large-language-models/3.1-pretraining-at-scale.md) | Data pipelines, training objective, distributed training, base vs instruct models |
| [3.2 Alignment: SFT, RLHF, DPO](./phase-3-large-language-models/3.2-alignment-sft-rlhf-dpo.md) | Full post-training pipeline, DPO vs RLHF, RLVR for reasoning |
| [3.3 Tokenization](./phase-3-large-language-models/3.3-tokenization.md) | BPE algorithm, why models fail at letter counting, token costs, chat templates |
| [3.4 Context windows & KV-cache](./phase-3-large-language-models/3.4-context-windows-kv-cache.md) | KV-cache memory math, lost-in-the-middle, prompt caching, serving strategies |
| [3.5 Hallucinations](./phase-3-large-language-models/3.5-hallucinations.md) | Root causes, taxonomy, RAG + tool use + citation requirements as defense |
| [3.6 Scaling laws & emergence](./phase-3-large-language-models/3.6-scaling-laws-and-emergence.md) | Kaplan, Chinchilla, inference scaling, emergent capabilities |

**Key insight:** Hallucinations aren't bugs — they're a structural property of how LLMs work. An LLM is a next-token predictor trained to be *plausible*, not *correct*. Understanding this is the difference between an engineer who blames the model and one who builds systems that compensate for it.

**Models to Know (as of 2026):**

| Provider | Model Family | Context Window | Strengths |
|---|---|---|---|
| Anthropic | Claude 4.x (Sonnet, Opus, Haiku) | Up to 1M tokens | Reasoning, coding, safety |
| OpenAI | GPT-4o, o3, o4-mini | 128K–1M tokens | Broad capabilities, ecosystem |
| Google | Gemini 2.x (Flash, Pro, Ultra) | 1M+ tokens | Multimodal, long context |
| Meta | Llama 4 | 128K+ tokens | Open weights, self-hosting |
| Mistral | Mixtral, Mistral Large | 128K tokens | Efficient, open weights |
| Alibaba | Qwen 2.5 | 128K+ tokens | Strong multilingual |

**Resources:**
- [Anthropic's model documentation](https://docs.anthropic.com)
- [Chinchilla scaling laws paper](https://arxiv.org/abs/2203.15556)
- [InstructGPT paper](https://arxiv.org/abs/2203.02155) — how RLHF actually works

---

## Phase 4 — Prompt Engineering

> The craft of talking to LLMs in a way that gets reliable results.
>
> → **[Full Phase 4 content with all sections](./phase-4-prompt-engineering/README.md)**

| Topic | What You'll Learn |
|---|---|
| [4.1 Prompt anatomy](./phase-4-prompt-engineering/4.1-prompt-anatomy.md) | System/user/assistant turns, assistant prefill, authority hierarchy, production templates |
| [4.2 Few-shot, CoT & structured prompting](./phase-4-prompt-engineering/4.2-few-shot-cot-structured-prompting.md) | Few-shot, chain-of-thought, self-consistency, dynamic few-shot, XML structure |
| [4.3 Output formatting](./phase-4-prompt-engineering/4.3-output-formatting-json-tools.md) | JSON schema enforcement, tool calls, Pydantic + Instructor, streaming structured output |
| [4.4 Failure modes & debugging](./phase-4-prompt-engineering/4.4-failure-modes-and-debugging.md) | 7-category failure taxonomy, bisect method, eval suites, consistency testing |
| [4.5 Prompt injection & defense](./phase-4-prompt-engineering/4.5-prompt-injection-and-defense.md) | OWASP LLM Top 10, direct/indirect injection, defense-in-depth, safe agent patterns |

**Key insight:** Prompt engineering is not "writing magic words." It's specifying behavior precisely enough that the model's training distribution aligns with what you want. If your prompt looks like instructions you'd give an intern, you're on the right track. If it looks like an incantation, you're going to have a bad time in production.

**The chain-of-thought finding (Wei et al., 2022):** Asking the model to reason step-by-step before answering dramatically improves accuracy on reasoning tasks. This isn't magic — it gives the model more output tokens to "think" in, and the reasoning constrains subsequent tokens.

```python
# Bad prompt — model has no room to reason
prompt = "Is 17 a prime number? Answer yes or no."

# Better prompt — gives the model reasoning space
prompt = """Is 17 a prime number? 
Think through the problem step by step, 
then give your final answer."""
```

**Resources:**
- [Anthropic Prompt Engineering Guide](https://docs.anthropic.com/en/docs/build-with-claude/prompt-engineering/overview)
- [OpenAI Prompt Engineering Guide](https://platform.openai.com/docs/guides/prompt-engineering)
- [Prompt Injection: Simon Willison's ongoing coverage](https://simonwillison.net/series/prompt-injection/)

---

## Phase 5 — Building with LLM APIs

> Writing production code against AI provider APIs.
>
> → **[Full Phase 5 content with all sections](./phase-5-building-with-llm-apis/README.md)**

| Topic | What You'll Learn |
|---|---|
| [5.1 Provider APIs](./phase-5-building-with-llm-apis/5.1-provider-apis.md) | Anthropic/OpenAI/Gemini SDKs, model routing, batch API, pricing comparison 2026 |
| [5.2 Streaming & async](./phase-5-building-with-llm-apis/5.2-streaming-and-async.md) | SSE mechanics, async FastAPI streaming, concurrent requests, TTFT optimization |
| [5.3 Token counting & cost](./phase-5-building-with-llm-apis/5.3-token-counting-and-cost.md) | Per-user attribution, budget enforcement, cost projection, 6 optimization levers |
| [5.4 Prompt caching](./phase-5-building-with-llm-apis/5.4-prompt-caching.md) | Anthropic/OpenAI/Google caching, 50–90% savings, stable prefix design |
| [5.5 Errors & retries](./phase-5-building-with-llm-apis/5.5-errors-retries-rate-limits.md) | Jitter backoff, circuit breakers, multi-provider fallback, thundering herd |
| [5.6 Multimodal](./phase-5-building-with-llm-apis/5.6-multimodal.md) | Images, PDFs, audio APIs — cost, optimization, caching, batch processing |

**Key insight:** The thing that will bite you in production isn't the AI part — it's the infrastructure part. Rate limits hit at the worst time. Streaming breaks in ways that are hard to reproduce. Token costs scale non-linearly with context. Build for these from day one.

```python
import anthropic
from tenacity import retry, stop_after_attempt, wait_exponential

client = anthropic.Anthropic()

@retry(
    stop=stop_after_attempt(3),
    wait=wait_exponential(multiplier=1, min=4, max=10)
)
def call_claude(system: str, user: str, model: str = "claude-sonnet-4-6") -> str:
    message = client.messages.create(
        model=model,
        max_tokens=1024,
        system=system,
        messages=[{"role": "user", "content": user}]
    )
    return message.content[0].text


# Streaming example
def stream_claude(system: str, user: str):
    with client.messages.stream(
        model="claude-sonnet-4-6",
        max_tokens=1024,
        system=system,
        messages=[{"role": "user", "content": user}]
    ) as stream:
        for text in stream.text_stream:
            print(text, end="", flush=True)
```

**Provider SDK Quick Reference:**

| Provider | SDK Install | Docs |
|---|---|---|
| Anthropic | `pip install anthropic` | docs.anthropic.com |
| OpenAI | `pip install openai` | platform.openai.com/docs |
| Google Gemini | `pip install google-genai` | ai.google.dev/docs |
| Cohere | `pip install cohere` | docs.cohere.com |

---

## Phase 6 — Embeddings & Semantic Search

> Making text searchable by meaning, not just keyword matching.
>
> → **[Full Phase 6 content with all sections](./phase-6-embeddings-semantic-search/README.md)**

| Topic | What You'll Learn |
|---|---|
| [6.1 What are embeddings?](./phase-6-embeddings-semantic-search/6.1-what-are-embeddings.md) | Meaning as vectors, contextual vs static, contrastive training, dimensionality |
| [6.2 Embedding models](./phase-6-embeddings-semantic-search/6.2-embedding-models.md) | Voyage/OpenAI/Cohere/BGE comparison, MTEB, asymmetric models, offline evaluation |
| [6.3 Similarity search](./phase-6-embeddings-semantic-search/6.3-similarity-search.md) | Cosine vs dot product, ANN algorithms (HNSW/IVF), recall-latency tradeoff |
| [6.4 Vector databases](./phase-6-embeddings-semantic-search/6.4-vector-databases.md) | Qdrant/pgvector/Pinecone/Weaviate — decision framework, full code examples |
| [6.5 Chunking strategies](./phase-6-embeddings-semantic-search/6.5-chunking-strategies.md) | Recursive splitting, semantic, parent-child, per-document-type guidance |
| [6.6 Hybrid search](./phase-6-embeddings-semantic-search/6.6-hybrid-search.md) | BM25 + dense, RRF fusion, dynamic alpha, reranking pipeline |

**Key insight:** The chunking strategy is the most underestimated decision in any RAG system. Naive fixed-size chunking with overlap works in demos and fails in production when your documents have complex structure. Invest in this early.

**Vector DB Comparison:**

| Database | Hosting | Best For | Pricing |
|---|---|---|---|
| Pinecone | Managed cloud | Production, teams, no infra overhead | Serverless pay-per-use |
| Weaviate | Self-host or cloud | Complex data models, hybrid search | Open source + cloud |
| Qdrant | Self-host or cloud | High performance, Rust-based | Open source + cloud |
| Chroma | Local / self-host | Development, prototyping | Open source |
| pgvector | PostgreSQL extension | You already run Postgres | Free (your Postgres cost) |
| Redis Stack | Self-host or cloud | Low latency, cache + vector | Redis pricing |

**Embedding Model Comparison:**

| Model | Provider | Dimensions | Context | Notes |
|---|---|---|---|---|
| text-embedding-3-large | OpenAI | 3072 | 8191 tokens | Strong general purpose |
| text-embedding-3-small | OpenAI | 1536 | 8191 tokens | Cost-efficient |
| embed-v4.0 | Cohere | 1024 | 512 tokens | Strong retrieval |
| all-MiniLM-L6-v2 | Hugging Face | 384 | 256 tokens | Fast, free, local |
| nomic-embed-text | Nomic | 768 | 8192 tokens | Open, strong performance |

---

## Phase 7 — RAG (Retrieval-Augmented Generation)

> The most important pattern in production AI engineering right now.
>
> → **[Full Phase 7 content with all sections](./phase-7-rag/README.md)**

| Topic | What You'll Learn |
|---|---|
| [7.1 RAG fundamentals](./phase-7-rag/7.1-rag-fundamentals.md) | When RAG, when not, two-phase architecture, decision framework |
| [7.2 Naive RAG](./phase-7-rag/7.2-naive-rag.md) | Complete indexing pipeline, query pipeline, citation patterns |
| [7.3 Advanced RAG](./phase-7-rag/7.3-advanced-rag.md) | Reranking, multi-query, HyDE, contextual compression — ROI per technique |
| [7.4 Agentic RAG](./phase-7-rag/7.4-agentic-rag.md) | Retrieval as tool call, multi-source routing, iteration limits |
| [7.5 RAG evaluation](./phase-7-rag/7.5-rag-evaluation.md) | RAGAS metrics, eval dataset design, LLM-as-judge, continuous monitoring |
| [7.6 RAG failure modes](./phase-7-rag/7.6-rag-failure-modes.md) | 10-mode diagnostic framework with targeted code fixes |

**The naive RAG pipeline:**

```
User Query
    │
    ▼
Embed Query ──────────────────────────────────────────┐
    │                                                  │
    ▼                                                  │
Vector DB: find top-K similar chunks                   │
    │                                                  │
    ▼                                                  │
Retrieved Context (chunks)                             │
    │                                                  │
    ▼                                                  │
Prompt: [System] + [Context] + [Query] ◄───────────────┘
    │
    ▼
LLM generates answer grounded in retrieved context
    │
    ▼
Response to user
```

**Key insight:** The thing nobody tells you about RAG is that retrieval is almost always your biggest quality bottleneck — not the LLM. If you're not retrieving the right chunks, the best model in the world can't save you. Invest 80% of your optimization effort in retrieval quality before touching the generation step.

**RAG Evaluation Metrics:**

| Metric | What it measures | Tool |
|---|---|---|
| Context Precision | Are retrieved chunks actually relevant? | RAGAS, TruLens |
| Context Recall | Did you retrieve everything needed to answer? | RAGAS |
| Answer Faithfulness | Does the answer stick to the retrieved context? | RAGAS, DeepEval |
| Answer Relevance | Does the answer actually address the question? | RAGAS |

**Frameworks:**

| Framework | Best For |
|---|---|
| LangChain | General RAG pipelines, large ecosystem |
| LlamaIndex | Document-heavy RAG, complex indexing |
| Haystack | Production-grade, strong eval integration |
| DSPy | Programmatic prompt optimization + RAG |
| Raw SDK | When you need control and don't want framework magic |

---

## Phase 8 — Tool Use & AI Agents

> Building systems where LLMs take actions, not just generate text.
>
> → **[Full Phase 8 content with all sections](./phase-8-tool-use-agents/README.md)**

| Topic | What You'll Learn |
|---|---|
| [8.1 Function calling & tool use](./phase-8-tool-use-agents/8.1-function-calling-tool-use.md) | Full tool-use loop, parallel calls, tool_choice forcing, MCP |
| [8.2 Designing good tools](./phase-8-tool-use-agents/8.2-designing-good-tools.md) | Names, descriptions, schemas, confirmation patterns, tool set design |
| [8.3 Single-agent patterns](./phase-8-tool-use-agents/8.3-single-agent-patterns.md) | ReAct + Reflexion, Plan-and-Execute, when to use each |
| [8.4 Multi-agent systems](./phase-8-tool-use-agents/8.4-multi-agent-systems.md) | Orchestrator-worker, handoffs, parallel execution, LangGraph |
| [8.5 Agent memory](./phase-8-tool-use-agents/8.5-agent-memory.md) | Short-term window, long-term semantic store, episodic memory |
| [8.6 Failure modes & guardrails](./phase-8-tool-use-agents/8.6-agent-failure-modes-guardrails.md) | 8-mode taxonomy, defense-in-depth guardrail architecture |

**Key insight:** Agents are powerful and unreliable in equal measure. The difference between a demo and a production agent is: error handling, state management, cost bounds, and knowing when to ask a human. If your agent can take irreversible actions (send email, write to DB, call APIs), you need explicit confirmation steps before those actions.

```python
import anthropic
import json

client = anthropic.Anthropic()

# Define tools the model can call
tools = [
    {
        "name": "get_weather",
        "description": "Get the current weather for a location",
        "input_schema": {
            "type": "object",
            "properties": {
                "location": {
                    "type": "string",
                    "description": "City and country, e.g. 'London, UK'"
                }
            },
            "required": ["location"]
        }
    }
]

def run_agent(user_message: str) -> str:
    messages = [{"role": "user", "content": user_message}]
    
    while True:
        response = client.messages.create(
            model="claude-sonnet-4-6",
            max_tokens=1024,
            tools=tools,
            messages=messages
        )
        
        # If model is done, return the text
        if response.stop_reason == "end_turn":
            return response.content[0].text
        
        # If model wants to call a tool, execute it
        if response.stop_reason == "tool_use":
            tool_use_block = next(b for b in response.content if b.type == "tool_use")
            tool_result = execute_tool(tool_use_block.name, tool_use_block.input)
            
            # Feed the result back to the model
            messages.append({"role": "assistant", "content": response.content})
            messages.append({
                "role": "user",
                "content": [{
                    "type": "tool_result",
                    "tool_use_id": tool_use_block.id,
                    "content": json.dumps(tool_result)
                }]
            })
```

**Agent Frameworks:**

| Framework | Model-Agnostic | Multi-Agent | Production-Ready | Notes |
|---|---|---|---|---|
| LangGraph | Yes | Yes | Yes | Best for complex stateful agents |
| AutoGen (Microsoft) | Yes | Yes | Maturing | Strong multi-agent support |
| CrewAI | Yes | Yes | Yes | Role-based multi-agent |
| Claude Code SDK | Anthropic-first | Yes | Yes | Anthropic's own agentic SDK |
| Raw SDK | Yes | DIY | Yes | Maximum control, more code |

---

## Phase 9 — Evals & Quality

> The discipline that separates AI engineering from AI experimentation.
>
> → **[Full Phase 9 content with all sections](./phase-9-evals-quality/README.md)**

| Topic | What You'll Learn |
|---|---|
| [9.1 Why evals are hard](./phase-9-evals-quality/9.1-why-evals-are-hard.md) | 6 core challenges, maturity ladder, the eval-investment math |
| [9.2 Types of evals](./phase-9-evals-quality/9.2-types-of-evals.md) | Deterministic/statistical/human/LLM-judge — the eval pyramid |
| [9.3 Building eval datasets](./phase-9-evals-quality/9.3-building-eval-datasets.md) | 5 sources, composition guidelines, versioning, canary cases |
| [9.4 LLM-as-judge](./phase-9-evals-quality/9.4-llm-as-judge.md) | Bias taxonomy, pairwise comparison, calibration, CoT judging |
| [9.5 Regression testing](./phase-9-evals-quality/9.5-regression-testing.md) | Statistical tests, GitHub Actions CI/CD gate, pytest integration |
| [9.6 Tracing & observability](./phase-9-evals-quality/9.6-tracing-and-observability.md) | Langfuse/Helicone/LangSmith setup, cost alerting, dashboards |

**Key insight:** You cannot improve what you cannot measure. Every AI team that skips evals early spends 3x longer fixing problems later because they have no way to tell if a change made things better or worse. Build your eval harness before you build your feature.

**Eval Tools:**

| Tool | Type | Best For |
|---|---|---|
| RAGAS | Open source | RAG-specific evaluation metrics |
| DeepEval | Open source | General LLM eval framework |
| LangSmith | Managed cloud | LangChain ecosystem, tracing + evals |
| Langfuse | Open source / cloud | Tracing, prompt management, evals |
| Helicone | Managed cloud | Cost tracking, caching, observability |
| Braintrust | Managed cloud | AI eval platform with CI integration |
| Weights & Biases | Managed cloud | ML experiment tracking + evals |

---

## Phase 10 — MLOps & Production AI

> Running AI systems in production without waking up to alerts at 3am.
>
> → **[Full Phase 10 content with all sections](./phase-10-mlops-production/README.md)**

| Topic | What You'll Learn |
|---|---|
| [10.1 Experiment tracking](./phase-10-mlops-production/10.1-experiment-tracking.md) | MLflow 3.0 GenAI features, W&B sweeps, prompt versioning |
| [10.2 Model registries](./phase-10-mlops-production/10.2-model-registries-versioning.md) | Semantic versioning, blue-green deployment, DVC for artifacts |
| [10.3 Training data management](./phase-10-mlops-production/10.3-feature-stores-training-data.md) | Versioned datasets, quality validation, feature stores |
| [10.4 CI/CD for ML](./phase-10-mlops-production/10.4-cicd-for-ml.md) | Four-gate pipeline, GitHub Actions YAML, eval gates, canary deploy |
| [10.5 Model monitoring](./phase-10-mlops-production/10.5-model-monitoring.md) | Five drift types, Page-Hinkley detection, cost + quality alerts |
| [10.6 A/B testing AI](./phase-10-mlops-production/10.6-ab-testing-ai-features.md) | Sample size calculation, statistical analysis, guardrail metrics |

**The three things that go wrong in production AI:**
1. **Data drift** — the real-world data distribution shifted and your model doesn't know
2. **Model rot** — the LLM provider updated their model and behavior changed silently
3. **Prompt brittleness** — a change in user behavior hits an edge case your prompt never saw

All three require monitoring to catch. None of them are caught by unit tests.

---

## Phase 11 — Fine-Tuning

> When prompt engineering isn't enough and you need the model to learn from your data.
>
> → **[Full Phase 11 content with all sections](./phase-11-fine-tuning/README.md)**

| Topic | What You'll Learn |
|---|---|
| [11.1 When to fine-tune](./phase-11-fine-tuning/11.1-when-to-fine-tune.md) | Decision framework: prompting → RAG → fine-tune; what fine-tuning can't fix |
| [11.2 Supervised fine-tuning](./phase-11-fine-tuning/11.2-supervised-fine-tuning.md) | Loss masking, chat templates, data prep pipeline, quality over quantity |
| [11.3 LoRA & QLoRA](./phase-11-fine-tuning/11.3-lora-and-qlora.md) | Low-rank adaptation math, 4-bit quantization, GPU requirements, Axolotl config |
| [11.4 API fine-tuning](./phase-11-fine-tuning/11.4-fine-tuning-apis.md) | OpenAI + Together AI APIs, cost estimation, weights ownership |
| [11.5 Evaluating fine-tuned models](./phase-11-fine-tuning/11.5-evaluating-fine-tuned-models.md) | Baseline comparison, forgetting check, training curve analysis |
| [11.6 Fine-tuning failures](./phase-11-fine-tuning/11.6-fine-tuning-failures.md) | 6 failure modes with diagnostics: insufficient data, inconsistent labels, forgetting |

**Key insight:** Fine-tune for style/format/domain adaptation. Don't fine-tune to add knowledge (use RAG for that). The most common fine-tuning mistake is treating it as a shortcut for prompt engineering. It isn't. You need at minimum hundreds, preferably thousands of high-quality examples.

**Fine-Tuning Options:**

| Option | GPU Required | Data Size Needed | Best For |
|---|---|---|---|
| OpenAI fine-tuning API | No | ~100–1000 examples | Quick, managed, GPT-based |
| Anthropic fine-tuning | No | Contact Anthropic | Claude customization |
| LoRA with Axolotl | Yes | ~500–5000 examples | Open models, full control |
| QLoRA (4-bit) | Consumer GPU | ~500+ examples | Limited GPU memory |
| Full fine-tune | Multi-GPU | ~10K+ examples | Maximum customization |

---

## Phase 12 — Deployment & Infrastructure

> Getting models into production and keeping them there.
>
> → **[Full Phase 12 content with all sections](./phase-12-deployment-infrastructure/README.md)**

| Topic | What You'll Learn |
|---|---|
| [12.1 Model serving](./phase-12-deployment-infrastructure/12.1-model-serving-frameworks.md) | vLLM, SGLang, Triton — production setup, OpenAI-compatible API |
| [12.2 GPU memory & batching](./phase-12-deployment-infrastructure/12.2-gpu-memory-batching-throughput.md) | PagedAttention, continuous batching, throughput benchmarking |
| [12.3 Quantization](./phase-12-deployment-infrastructure/12.3-quantization.md) | INT8, INT4, FP8, GPTQ vs AWQ — quality trade-off tables |
| [12.4 Distributed inference](./phase-12-deployment-infrastructure/12.4-distributed-inference.md) | Tensor parallelism, pipeline parallelism, speculative decoding |
| [12.5 Latency vs throughput](./phase-12-deployment-infrastructure/12.5-latency-vs-throughput.md) | TTFT vs TBT, SLA configuration, tail latency, priority queues |
| [12.6 Cost optimization](./phase-12-deployment-infrastructure/12.6-cost-optimization.md) | Prefix caching, semantic cache, model routing, 6-layer cost stack |

**Self-Hosting vs Managed API:**

| Factor | Use Managed API | Self-Host |
|---|---|---|
| Team size | Small, moving fast | Large, cost-sensitive |
| Cost at scale | Lower initially | Lower at high volume |
| Data privacy | Acceptable to send to provider | Data cannot leave your infra |
| Model control | Fine with provider's model | Need specific weights |
| Ops burden | Avoid it | Can handle it |

**vLLM quickstart (self-hosting Llama):**
```bash
pip install vllm

# Serve a model (requires GPU)
python -m vllm.entrypoints.openai.api_server \
    --model meta-llama/Llama-3-8B-Instruct \
    --port 8000

# It exposes an OpenAI-compatible API
curl http://localhost:8000/v1/chat/completions \
    -H "Content-Type: application/json" \
    -d '{"model": "meta-llama/Llama-3-8B-Instruct", "messages": [{"role": "user", "content": "Hello"}]}'
```

---

## Essential Python Stack

```
Core AI SDKs
├── anthropic              # Claude API
├── openai                 # OpenAI + OpenAI-compatible APIs
├── google-genai           # Gemini
└── cohere                 # Cohere embeddings + generation

RAG & Embeddings
├── langchain              # General LLM pipelines
├── llama-index            # Document indexing + RAG
├── sentence-transformers  # Local embedding models
└── chromadb               # Local vector store (dev)

Vector DBs (pick one for prod)
├── pinecone-client        # Managed cloud vector DB
├── weaviate-client        # Self-host or cloud
└── qdrant-client          # High-perf self-host or cloud

Evals & Observability
├── ragas                  # RAG evaluation metrics
├── deepeval               # LLM eval framework
├── langfuse               # Tracing + observability
└── mlflow                 # Experiment tracking

Agents
├── langgraph              # Stateful agent graphs
└── crewai                 # Role-based multi-agent

Utilities
├── tenacity               # Retry logic
├── tiktoken               # Token counting (OpenAI models)
└── pydantic               # Data validation + structured output
```

---

## Projects to Build (In Order)

Building things is how this sticks. Here are projects mapped to the phases:

| Phase | Project | What You'll Practice |
|---|---|---|
| 1–3 | Train a small transformer from scratch (follow Karpathy's nanoGPT) | Mechanics of transformers |
| 4 | Build a prompt library with eval scripts | Prompt engineering + eval basics |
| 5 | CLI chatbot with streaming, retry, and cost tracking | Production API usage |
| 6 | Semantic search over your notes / a document set | Embeddings + vector DB |
| 7 | RAG system over a PDF collection with eval metrics | Full RAG pipeline |
| 8 | Agent that can search the web, read files, write code | Tool use + agent loops |
| 9 | Eval harness for one of your previous projects | Evaluation infrastructure |
| 10 | Add observability + a/b testing to a project | Production AI ops |
| 11 | Fine-tune a small open model on a specific task | Fine-tuning end-to-end |
| 12 | Self-host a small model with vLLM | Deployment + serving |

---

## The Papers You Should Actually Read

These aren't homework. These are the papers that changed how the field works.

| Paper | Why It Matters |
|---|---|
| Attention Is All You Need (Vaswani et al., 2017) | Invented the transformer |
| BERT (Devlin et al., 2018) | Encoder-only models, bidirectional context |
| GPT-3 (Brown et al., 2020) | Showed few-shot learning at scale |
| InstructGPT (Ouyang et al., 2022) | How RLHF makes models useful |
| Chain-of-Thought Prompting (Wei et al., 2022) | Why CoT works |
| Chinchilla (Hoffmann et al., 2022) | Scaling laws: compute-optimal training |
| RAG (Lewis et al., 2020) | The original RAG paper |
| LoRA (Hu et al., 2021) | Parameter-efficient fine-tuning |
| Constitutional AI (Bai et al., 2022) | Anthropic's approach to alignment |

---

## Communities & Where to Stay Current

The field moves monthly. Staying current isn't optional.

- **Twitter/X:** @karpathy, @ylecun, @emollick, @simonw, @swyx, @hwchase17
- **Newsletters:** The Batch (deeplearning.ai), Import AI, TLDR AI, The Pragmatic Engineer
- **Discord:** Latent Space, Hugging Face, LangChain Discord
- **Papers:** arxiv.org/list/cs.AI/recent — skim daily, deep-read weekly
- **Blogs:** Anthropic research blog, OpenAI research, Google DeepMind, Hugging Face blog

---

## Honest Advice From Someone Who's Been There

**On hype:** 80% of "AI engineering" blog posts describe demos, not production systems. Judge everything by: "has this held up under real traffic, real users, and real failure modes?"

**On frameworks:** LangChain and LlamaIndex will get you moving fast and will abstract away things you need to understand later. Learn the raw SDK first, then use frameworks when they save you time without hiding things you care about.

**On agents:** Everyone wants to build agents. Agents are the hardest thing to get right. Start with the simplest possible architecture (single LLM call) and only add agent complexity when you've hit a wall. Most things that look like "we need an agent" are solved by a better prompt and a retrieval step.

**On evals:** Build your eval before you build your feature. Non-negotiable. You cannot improve what you cannot measure.

**On cost:** Token costs will surprise you at scale. Run the math on your expected usage before you ship. Cache aggressively. Choose smaller models for tasks that don't need big models.

**On the job market:** The AI engineer who can debug a broken pipeline, write an eval suite, and explain why the model is failing is 10x more valuable than the one who can write a LangChain tutorial. The field needs engineers, not prompt-writers.

---

## Getting Help From This Curriculum

This README maps to an interactive teaching system. Use these commands:

```
teach me [topic]              → Deep dive on any roadmap topic
go deeper on [aspect]         → More detail on a specific part
compare [X] vs [Y]            → Side-by-side comparison
give me a real example of [X] → Production case study
what should I learn next?     → Recommended next step
ready to test                 → Switch to quiz mode
```

---

*Last updated: June 2026*
*Field changes fast. If something looks outdated, it probably is — ask for an update.*
