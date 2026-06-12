# Chapter 13 — Complete Tool Catalog

> Every tool, library, platform, and service in the AI engineering ecosystem — categorized, briefly described, and cross-referenced.

---

## 13.1 LLM SDKs & Clients

| Tool | Language | Provider | Notes |
|---|---|---|---|
| **anthropic** | Python/TS | Anthropic | Official; async support |
| **openai** | Python/TS | OpenAI | Official; async |
| **google-genai** | Python | Google | Replaced google-generativeai |
| **mistralai** | Python/TS | Mistral | Official |
| **cohere** | Python/TS | Cohere | Official |
| **groq** | Python/TS | Groq | Fast inference; OpenAI-compatible |
| **litellm** | Python | Unified | 100+ providers; single API |
| **langchain** | Python/TS | Multi | Chains + agents |
| **llama-index** | Python | Multi | RAG-focused |

---

## 13.2 Serving & Inference

| Tool | Type | Notes |
|---|---|---|
| **vLLM** | Serving framework | PagedAttention; default choice |
| **SGLang** | Serving framework | RadixAttention; agent workloads |
| **Triton Inference Server** | Multi-model server | NVIDIA; enterprise |
| **TensorRT-LLM** | Optimization library | NVIDIA H100 optimization |
| **TorchServe** | PyTorch serving | General PyTorch; not LLM-optimized |
| **llama.cpp** | CPU inference | GGUF format; any hardware |
| **Ollama** | Local serving | Wraps llama.cpp; developer-friendly |
| **LM Studio** | Local GUI | Desktop app for local models |
| **llamafile** | Single-file | Run any GGUF model as executable |
| **OpenLLM** (BentoML) | Cloud serving | BentoML-native |
| **LoRAX** | LoRA serving | Multiple adapters; one base model |
| **ktransformers** | CPU+GPU hybrid | Partial GPU offload optimization |

---

## 13.3 Orchestration & Agent Frameworks

| Tool | Notes |
|---|---|
| **LangChain** | Most ecosystem; chains + agents |
| **LangGraph** | Stateful graphs; production agents |
| **LlamaIndex** | Document + RAG focus |
| **CrewAI** | Role-based multi-agent |
| **AutoGen** | Microsoft; conversational multi-agent |
| **Semantic Kernel** | Microsoft; .NET + Python; Azure |
| **Haystack** | deepset; production RAG; strong eval |
| **DSPy** | Stanford; programmatic prompting |
| **OpenAI Agents SDK** | OpenAI-native; handoffs |
| **Anthropic Agent SDK** | Claude-native; MCP |
| **Flowise** | Low-code LangChain visual builder |
| **Dify** | Low-code LLM app platform |
| **PromptFlow** (Microsoft) | Azure-native pipeline builder |
| **Rivet** | Visual AI workflow editor |
| **n8n** | General automation + AI |
| **Activepieces** | Open-source automation + AI |

---

## 13.4 Vector Databases

| Tool | Type | Notes |
|---|---|---|
| **Qdrant** | Purpose-built | Rust; best new project default |
| **Pinecone** | Managed cloud | Zero-ops; enterprise SLAs |
| **Weaviate** | Purpose-built | Native hybrid; GraphQL |
| **Chroma** | Local/cloud | Developer-friendly |
| **Milvus** | Purpose-built | Billion-scale; Kubernetes |
| **pgvector** | Postgres extension | SQL-native |
| **Redis Stack** | Redis module | Low-latency; Redis ecosystem |
| **Deep Lake** | LLM-specific | Version-controlled; streaming |
| **LanceDB** | Embedded Rust | Serverless; columnar |
| **Turbopuffer** | Cloud | Serverless; cost-effective |
| **Faiss** | Library | Meta; offline batch |
| **Annoy** | Library | Spotify; read-optimized |
| **hnswlib** | Library | Fast HNSW |
| **ScaNN** | Library | Google; high dimensions |
| **usearch** | Library | Fast; modern |

---

## 13.5 Embedding Models

*(Full details in [Chapter 5](./05-embeddings-and-vector-tech.md))*

| Tool | Notes |
|---|---|
| **sentence-transformers** | PyTorch; 400+ models |
| **voyageai** | Voyage AI Python SDK |
| **FlagEmbedding** | BAAI; BGE models |
| **nomic-embed** | Nomic AI; open commercial |
| **fastembed** | Qdrant; fast CPU embedding |

---

## 13.6 Fine-Tuning Libraries

| Tool | Notes |
|---|---|
| **TRL** (HuggingFace) | SFT, DPO, PPO, GRPO; reference |
| **PEFT** (HuggingFace) | LoRA, QLoRA, adapters |
| **Axolotl** | Config-driven; best defaults |
| **torchtune** | Meta's official; pure PyTorch |
| **LLaMAFactory** | Easy; web UI available |
| **Unsloth** | 2–4× faster LoRA training |
| **OpenRLHF** | Large-scale RLHF/DPO |
| **veRL** | ByteDance; RLVR |
| **TRLX** | EleutherAI; RL for LLMs |
| **Lit-GPT** | Lightning AI; hackable |
| **nanoGPT** | Karpathy; educational |
| **bitsandbytes** | 8-bit + 4-bit quantization |
| **AutoAWQ** | AWQ quantization |
| **AutoGPTQ** | GPTQ quantization |

---

## 13.7 Evaluation & Testing

| Tool | Notes |
|---|---|
| **RAGAS** | RAG-specific; 10+ metrics |
| **DeepEval** | 30+ metrics; pytest integration |
| **TruLens** | TruEra; RAG triad |
| **Giskard** | Safety + quality; LLM scan |
| **PromptFoo** | CLI; multi-provider; YAML config |
| **Braintrust** | Commercial; CI/CD integration |
| **Patronus AI** | Commercial; hallucination detection |
| **Galileo** | Commercial; Luna hallucination |
| **Arthur Shield** | Safety evaluation |
| **Evals** (OpenAI) | OpenAI's own framework |
| **lm-evaluation-harness** (EleutherAI) | Standard academic eval |
| **Inspect** (UK AISI) | Safety evaluation |
| **AgentBench** | Multi-task agent evaluation |

---

## 13.8 Observability & Monitoring

| Tool | Notes |
|---|---|
| **Langfuse** | Open source; traces + prompts + evals |
| **LangSmith** | LangChain ecosystem; deep tracing |
| **Helicone** | Proxy; zero-code setup |
| **Arize Phoenix** | ML + LLM; drift detection |
| **Portkey** | Gateway + observability |
| **Datadog LLM** | Enterprise APM extension |
| **Honeycomb** | Event-based deep tracing |
| **Traceloop** | OpenTelemetry-based |
| **Literal AI** | Open source; chat traces |
| **Weights & Biases** | Experiments + prompts |
| **MLflow 3.0** | GenAI tracing + ML lifecycle |

---

## 13.9 Data Tools

| Tool | Category | Notes |
|---|---|---|
| **Argilla** | Annotation | NLP + LLM data annotation |
| **Label Studio** | Annotation | General; multi-modal |
| **Scale AI** | Annotation | Enterprise; RLHF data |
| **Prolific** | Crowdsource | Research participants |
| **DVC** | Versioning | Git for data/models |
| **lakeFS** | Versioning | Git-like data lake |
| **unstructured.io** | Parsing | Multi-format document parser |
| **docling** (IBM) | Parsing | Enterprise doc parsing |
| **markitdown** | Conversion | Any → Markdown |
| **pymupdf** | PDF | Best general PDF parser |
| **pdfplumber** | PDF | Tables from PDFs |
| **Hugging Face Datasets** | Hub | 50K+ datasets |
| **Datatrove** | Pipeline | Large-scale data processing |

---

## 13.10 MLOps Platforms

| Tool | Notes |
|---|---|
| **MLflow** | Open source; full lifecycle |
| **Weights & Biases** | Experiment tracking + artifacts |
| **Neptune.ai** | Metadata management |
| **Comet ML** | Experiment tracking |
| **ClearML** | Full MLOps; open source |
| **DagsHub** | Git + DVC + MLflow |
| **Feast** | Feature store |
| **Tecton** | Feature store; enterprise |
| **Airflow** | Pipeline orchestration |
| **Prefect** | Python-native orchestration |
| **Metaflow** | Netflix; ML-specific |
| **ZenML** | Cloud-agnostic ML pipelines |
| **Kubeflow** | Kubernetes-native ML |
| **Flyte** | Type-safe ML pipelines |
| **BentoML** | Model serving + MLOps |
| **Seldon Core** | Kubernetes model serving |
| **Databricks** | Lakehouse + MLflow |

---

## 13.11 Prompt Engineering Tools

| Tool | Notes |
|---|---|
| **Anthropic Console** | Claude prompt engineering UI |
| **OpenAI Playground** | GPT prompt testing |
| **PromptLayer** | Versioning + tracking |
| **Langfuse Prompts** | Production prompt management |
| **Braintrust** | Evals + prompt management |
| **PromptFlow** (Azure) | Visual prompt pipelines |
| **Dspy** | Programmatic optimization |
| **LMQL** | Programming language for LLMs |
| **Guidance** (Microsoft) | Constrained LLM generation |
| **Outlines** | Structured generation |

---

## 13.12 Security Tools

| Tool | Notes |
|---|---|
| **Garak** | Red-teaming; vulnerability scanning |
| **PromptBench** | Robustness testing |
| **Lakera Guard** | Real-time injection + safety |
| **Microsoft Prompt Shield** | Azure; injection detection |
| **NeMo Guardrails** | NVIDIA; topical/safety rails |
| **Guardrails AI** | Output validation + retry |
| **LLM Guard** | Multi-scanner pipeline |
| **Rebuff** | Injection detection |
| **TextAttack** | NLP adversarial attacks |

---

## 13.13 Coding Assistants & Developer Tools

| Tool | Notes |
|---|---|
| **GitHub Copilot** | Inline code completion; IDE |
| **Cursor** | AI-first code editor |
| **Windsurf** | Codeium; AI-first IDE |
| **Zed** | Fast editor; AI features |
| **Claude Code** | Anthropic; terminal + IDE |
| **Aider** | Git-aware CLI coding assistant |
| **Continue** | Open source; any IDE |
| **Codeium** | Free Copilot alternative |
| **Tabnine** | Privacy-first code completion |
| **Amazon Q Developer** | AWS-native |
| **Gemini Code Assist** | Google-native |

---

## 13.14 Deployment & Infrastructure

| Tool | Category | Notes |
|---|---|---|
| **Docker** | Containerization | Standard for model packaging |
| **Kubernetes** | Orchestration | Scale model serving |
| **Helm** | K8s package manager | Model deployment charts |
| **Ray** | Distributed compute | Ray Serve for model serving |
| **Replicate** | Cloud deployment | Easy model API hosting |
| **Modal** | Serverless GPU | Python-native; easy fine-tuning |
| **RunPod** | GPU cloud | Serverless + dedicated |
| **Fly.io** | Edge deployment | Global inference |
| **Cloudflare Workers AI** | Edge AI | Run models at the edge |
| **Vercel AI SDK** | JS/TS | Frontend AI integration |

---

## 13.15 Multimodal Tools

| Tool | Category | Notes |
|---|---|---|
| **Whisper** | ASR | OpenAI; best open speech-to-text |
| **Deepgram** | ASR | Real-time; accurate |
| **AssemblyAI** | ASR | Good diarization |
| **ElevenLabs** | TTS | Best voice quality |
| **DALL-E 3** | Text-to-image | OpenAI |
| **Stable Diffusion** | Text-to-image | Open source; self-host |
| **Midjourney** | Text-to-image | Best aesthetics |
| **Flux** | Text-to-image | Black Forest Labs; open |
| **Sora** | Text-to-video | OpenAI |
| **Gen-3** | Text-to-video | RunwayML |
| **Florence-2** | Vision encoder | Microsoft; efficient |
| **LLaVA** | Vision-language | Open; multimodal |

---

## 13.16 Useful Python Libraries

| Library | Category | Notes |
|---|---|---|
| **tiktoken** | Tokenization | OpenAI fast tokenizer |
| **transformers** | Models | HuggingFace; 500K+ models |
| **datasets** | Data | HuggingFace dataset hub |
| **accelerate** | Training | Multi-GPU; mixed precision |
| **sentence-transformers** | Embeddings | Pre-trained embedding models |
| **faiss-cpu/gpu** | ANN search | Meta; fast similarity search |
| **hnswlib** | ANN search | HNSW implementation |
| **rank-bm25** | BM25 | Sparse retrieval |
| **tenacity** | Retry | Best Python retry library |
| **pydantic** | Validation | Data validation + settings |
| **httpx** | HTTP | Async HTTP client |
| **pytest** | Testing | With eval plugins |
| **numpy** | Numerics | Array operations |
| **scipy** | Scientific | Statistics, clustering |
| **instructor** | Structured output | Pydantic + LLM validation |

---

*[← Chapter 12: Key Papers & Benchmarks](./12-key-papers-and-benchmarks.md) | [Back to Bible Index →](./README.md)*

*Sources: [alexbobes.com — 150+ LLM Tools](https://alexbobes.com/artificial-intelligence/the-ultimate-llm-engineer-toolkit/) · [tiptinker — AI Engineering Stack 2026](https://www.tiptinker.com/llm-frameworks/) · [kellton — AI Tech Stack 2026](https://www.kellton.com/kellton-tech-blog/ai-tech-stack-2026)*
