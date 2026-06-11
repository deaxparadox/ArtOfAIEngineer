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

```
PHASE 1 — ML Foundations
PHASE 2 — Deep Learning
PHASE 3 — Large Language Models
PHASE 4 — Prompt Engineering
PHASE 5 — Building with LLM APIs
PHASE 6 — Embeddings & Semantic Search
PHASE 7 — RAG (Retrieval-Augmented Generation)
PHASE 8 — Tool Use & AI Agents
PHASE 9 — Evals & Quality
PHASE 10 — MLOps & Production AI
PHASE 11 — Fine-Tuning
PHASE 12 — Deployment & Infrastructure
```

---

## Phase 1 — ML Foundations

> What you need to understand before any of this makes sense.

| Topic | What You'll Learn |
|---|---|
| 1.1 What is machine learning? | Types and taxonomy: supervised, unsupervised, reinforcement |
| 1.2 How neural networks learn | Forward pass, loss functions, backpropagation |
| 1.3 Gradient descent & optimizers | SGD, Adam, AdamW — why they exist and when they fail |
| 1.4 Overfitting & evaluation | Regularization, train/val/test splits, precision/recall/F1 |
| 1.5 ML → Deep Learning | How scale and data changed what's possible |

**Key insight:** You don't need to implement backprop from scratch. You need to understand it well enough to know *why* your training loss is behaving the way it is.

**Resources:**
- [fast.ai Practical Deep Learning](https://course.fast.ai) — bottom-up, code-first
- [3Blue1Brown Neural Networks playlist](https://www.youtube.com/playlist?list=PLZHQObOWTQDNU6R1_67000Dx_ZCJB-3pi) — best visual intuition available
- [StatQuest with Josh Starmer](https://www.youtube.com/@statquest) — for the stats underpinning

---

## Phase 2 — Deep Learning

> The architectural building blocks that everything else is built on.

| Topic | What You'll Learn |
|---|---|
| 2.1 CNNs | Convolutional layers, pooling, image feature extraction |
| 2.2 RNNs & LSTMs | Sequential data, memory, the vanishing gradient problem |
| 2.3 The Attention Mechanism | The idea that broke everything open in 2017 |
| 2.4 The Transformer Architecture | Encoder, decoder, multi-head attention, positional encoding |
| 2.5 Transfer Learning | Why fine-tuning pre-trained models beats training from scratch |

**Key insight:** Read the original "Attention Is All You Need" paper (Vaswani et al., 2017). Not because you'll implement it, but because understanding *why* transformers replaced RNNs tells you exactly what LLMs are good and bad at.

**Resources:**
- [The Illustrated Transformer — Jay Alammar](https://jalammar.github.io/illustrated-transformer/)
- [Andrej Karpathy: Let's build GPT from scratch](https://www.youtube.com/watch?v=kCc8FmEb1nY) — the single best resource for understanding transformers
- [PyTorch documentation](https://pytorch.org/docs/stable/index.html)

---

## Phase 3 — Large Language Models

> How LLMs are built, what they actually are, and why they behave the way they do.

| Topic | What You'll Learn |
|---|---|
| 3.1 Pre-training at scale | How LLMs learn to predict text on trillions of tokens |
| 3.2 Alignment: SFT, RLHF, DPO | How raw models become useful assistants |
| 3.3 Tokenization | BPE, WordPiece — how text becomes numbers (and why this causes bugs) |
| 3.4 Context windows & KV-cache | Why context size matters, what KV-cache is, memory tradeoffs |
| 3.5 Hallucinations | Root causes, why they're structural, mitigation strategies |
| 3.6 Scaling laws & emergence | Why bigger models behave qualitatively differently |

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

| Topic | What You'll Learn |
|---|---|
| 4.1 Prompt anatomy | System prompt, user turn, assistant turn, message structure |
| 4.2 Prompting techniques | Zero-shot, few-shot, chain-of-thought, self-consistency |
| 4.3 Structured output | JSON mode, tool calls, forcing schema-compliant output |
| 4.4 Failure mode diagnosis | Why prompts fail and how to systematically debug them |
| 4.5 Prompt security | Injection attacks, jailbreaks, input sanitization |

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

| Topic | What You'll Learn |
|---|---|
| 5.1 Provider APIs | Anthropic SDK, OpenAI SDK, Gemini SDK — real usage patterns |
| 5.2 Streaming | Server-sent events, async generators, UI streaming patterns |
| 5.3 Token counting & cost | Counting tokens before sending, estimating costs, budget guardrails |
| 5.4 Prompt caching | When to cache, how it works, the savings you can expect |
| 5.5 Errors & retries | Rate limit handling, exponential backoff, fallback providers |
| 5.6 Multimodal | Sending images, PDFs, audio — what the APIs actually support |

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

| Topic | What You'll Learn |
|---|---|
| 6.1 What are embeddings? | From tokens to vectors — what they represent and why |
| 6.2 Embedding models | Choosing between providers and open-source options |
| 6.3 Similarity search | Cosine similarity, dot product, Euclidean distance |
| 6.4 Vector databases | Pinecone, Weaviate, Qdrant, Chroma, pgvector |
| 6.5 Chunking strategies | Character, token, sentence, semantic — which to use when |
| 6.6 Hybrid search | Combining dense vector search with BM25 keyword search |

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

| Topic | What You'll Learn |
|---|---|
| 7.1 RAG fundamentals | Why it exists: grounding LLMs in real, current, private data |
| 7.2 Naive RAG | The basic pipeline: embed → store → retrieve → generate |
| 7.3 Advanced RAG | Reranking, query expansion, HyDE, multi-query |
| 7.4 Agentic RAG | When retrieval is a tool the agent calls, not a fixed pipeline step |
| 7.5 RAG evaluation | Context precision, context recall, answer faithfulness, answer relevance |
| 7.6 RAG failure modes | The 7 ways RAG fails in production and how to fix each |

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

| Topic | What You'll Learn |
|---|---|
| 8.1 Function calling | How tool use works under the hood, the API mechanics |
| 8.2 Designing good tools | Tool schemas, descriptions that the model can actually use |
| 8.3 Single-agent patterns | ReAct (Reason + Act), Plan-and-Execute |
| 8.4 Multi-agent systems | Orchestrator-subagent patterns, handoffs, shared state |
| 8.5 Agent memory | In-context, external DB, episodic memory patterns |
| 8.6 When agents fail | Failure modes, guardrails, kill switches, human-in-the-loop |

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

> The hardest part of AI engineering, and the part most teams skip until it burns them.

| Topic | What You'll Learn |
|---|---|
| 9.1 Why evals are hard | Non-determinism, subjective quality, the "it depends" problem |
| 9.2 Types of evals | Unit evals, integration evals, human eval, LLM-as-judge |
| 9.3 Building eval datasets | What makes a good eval set and what makes a useless one |
| 9.4 LLM-as-judge | How to set it up, where it works, where it lies to you |
| 9.5 Regression testing | Testing non-deterministic systems — the surprisingly solvable problem |
| 9.6 Observability | Tracing, logging, cost tracking for production AI systems |

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

| Topic | What You'll Learn |
|---|---|
| 10.1 Experiment tracking | MLflow, W&B, Comet — tracking runs, params, metrics |
| 10.2 Model registries | Versioning models, promoting between environments |
| 10.3 Training data management | Feature stores, lineage, versioning training data |
| 10.4 CI/CD for ML | Testing ML code, staging, deployment gates |
| 10.5 Model monitoring | Drift detection, performance degradation, anomaly detection |
| 10.6 A/B testing AI | How to run controlled experiments on AI features |

**The three things that go wrong in production AI:**
1. **Data drift** — the real-world data distribution shifted and your model doesn't know
2. **Model rot** — the LLM provider updated their model and behavior changed silently
3. **Prompt brittleness** — a change in user behavior hits an edge case your prompt never saw

All three require monitoring to catch. None of them are caught by unit tests.

---

## Phase 11 — Fine-Tuning

> When prompt engineering isn't enough and you need the model to learn from your data.

| Topic | What You'll Learn |
|---|---|
| 11.1 When to fine-tune | The honest answer: usually later than you think |
| 11.2 Supervised fine-tuning (SFT) | The data format, the training process, the compute requirements |
| 11.3 LoRA & QLoRA | Parameter-efficient fine-tuning — the technique that made fine-tuning accessible |
| 11.4 API fine-tuning | OpenAI, Anthropic, and others — managed fine-tuning without GPUs |
| 11.5 Evaluating fine-tuned models | Is your fine-tuned model actually better? How to know. |
| 11.6 Fine-tuning failure modes | The dataset size myth, catastrophic forgetting, overfitting |

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

| Topic | What You'll Learn |
|---|---|
| 12.1 Model serving | vLLM, TorchServe, Triton — the tradeoffs |
| 12.2 GPU memory & throughput | KV-cache, paged attention, batching strategies |
| 12.3 Quantization | INT8, INT4, GPTQ, AWQ — speed/quality tradeoffs |
| 12.4 Distributed inference | Tensor parallelism, pipeline parallelism |
| 12.5 Latency vs throughput | When to optimize for which — they pull in opposite directions |
| 12.6 Cost optimization | Caching, batching, model routing, dynamic model selection |

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
