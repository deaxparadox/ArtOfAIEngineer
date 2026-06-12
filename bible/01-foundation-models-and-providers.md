# Chapter 1 — Foundation Models & Providers

> Every major language model family, provider, and open-weight model — specs, pricing, context windows, strengths, and when to use each.

---

## 1.1 The Major Closed-Source Providers

### Anthropic — Claude Family

Anthropic was founded in 2021 by former OpenAI researchers. Constitutional AI (CAI) is their alignment approach — models are trained using a "constitution" of principles rather than purely human feedback. Claude models are generally considered the strongest for coding, long-context reasoning, and following nuanced instructions.

| Model | Context | Input ($/1M) | Output ($/1M) | Strengths |
|---|---|---|---|---|
| **claude-haiku-4-5** | 200K | $1.00 | $5.00 | Speed, classification, simple tasks |
| **claude-sonnet-4-6** | 200K | $3.00 | $15.00 | Best value; coding, reasoning |
| **claude-opus-4-8** | 1M | $15.00 | $75.00 | Most capable; complex reasoning |

**Signature features:**
- Extended thinking (internal chain-of-thought, budget_tokens configurable)
- 1M token context window on Opus
- Native tool use (Anthropic SDK format)
- Constitutional AI alignment
- Model Context Protocol (MCP) — Anthropic invented this standard
- Prompt caching with explicit cache_control markers (90% off cached tokens)
- Messages Batches API (50% off async workloads)

**Best for:** Complex reasoning, coding, long-document analysis, instruction-following, safety-critical applications

---

### OpenAI — GPT Family

OpenAI, founded 2015, pioneered the modern LLM era with GPT-3 (2020) and ChatGPT (2022). Their o-series models introduced inference-time compute scaling.

| Model | Context | Input ($/1M) | Output ($/1M) | Strengths |
|---|---|---|---|---|
| **gpt-4o-mini** | 128K | $0.15 | $0.60 | Cheapest capable model; high-volume |
| **gpt-4o** | 128K | $2.50 | $10.00 | Multimodal; broad capability |
| **o4-mini** | 200K | $1.10 | $4.40 | Fast reasoning; great value |
| **o3** | 200K | $10.00 | $40.00 | Best OpenAI reasoning |
| **gpt-5** | 1M (est.) | ~$2.50 | ~$10.00 | Latest flagship (Aug 2025) |

**Signature features:**
- Automatic prefix caching (1024+ token prompts, 50% off, no code changes)
- o-series: extended thinking, reasoning traces
- gpt-4o: native image + audio + text multimodal
- Batch API (50% off, 24hr turnaround)
- Fine-tuning API (SFT + DPO for gpt-4o-mini and gpt-4o)
- Assistants API (threads, file retrieval, code interpreter)
- DALL-E image generation, Whisper speech recognition, TTS

**Best for:** Multimodal tasks, broad general capability, tight OpenAI ecosystem integration

---

### Google DeepMind — Gemini Family

Google DeepMind merged Google Brain and DeepMind in 2023. Gemini models are natively multimodal and lead on long-context capabilities.

| Model | Context | Input ($/1M) | Output ($/1M) | Strengths |
|---|---|---|---|---|
| **gemini-2.5-flash** | 1M | $0.30 | $2.50 | Best cost-efficiency; speed |
| **gemini-2.5-flash-lite** | 1M | $0.10 | $0.40 | Cheapest; high throughput |
| **gemini-2.5-pro** | 2M | $2.50 | $15.00 | Longest context; multimodal |
| **gemini-3-pro** (est.) | 2M+ | TBD | TBD | Next generation flagship |

**Signature features:**
- 2M token context (Gemini 2.5 Pro — largest commercially available)
- Native video understanding (not just images)
- Context Caching API (configurable TTL, ~75% off cached tokens)
- Google Search grounding (real-time web access)
- Native multimodal: text + image + audio + video + code
- TPU training — JAX-optimized

**Best for:** Long-document processing, multimodal pipelines, Google Cloud integration

---

### xAI — Grok Family

xAI, founded by Elon Musk in 2023, has rapidly iterated to frontier-class models. Grok-4 leads SWE-bench and HLE benchmarks.

| Model | Context | Notes |
|---|---|---|
| **Grok 4** | 1M | SWE-bench leader (75%); best code and math |
| **Grok 3** | 128K | Production-ready; cost-efficient |

**Best for:** Coding and math tasks at lowest cost; X/Twitter integration

---

### Mistral AI — Mistral / Mixtral Family

European AI lab, founded 2023. Strong on efficiency, multilingual, and European data sovereignty.

| Model | Params | Context | Open? | Notes |
|---|---|---|---|---|
| **Mistral Large 2** | 123B | 128K | Yes | Best open-weights large model |
| **Mistral Small 3** | 24B | 128K | Yes | Efficient; good quality |
| **Codestral** | 22B | 32K | Yes | Optimized for code generation |
| **Mistral NeMo** | 12B | 128K | Yes | Good multilingual |
| **Mixtral 8×22B** | 141B total, 39B active | 65K | Yes | MoE; high quality/cost ratio |

**Best for:** European data residency, open-weight deployment, multilingual

---

## 1.2 Open-Weight Model Families

### Meta — LLaMA Family

Meta's open-weight models have been the most widely adopted open-source foundation models.

| Model | Type | Context | Active Params | Notes |
|---|---|---|---|---|
| **LLaMA 4 Scout** | MoE | 10M | 17B | Longest context open model |
| **LLaMA 4 Maverick** | MoE | 1M | ~100B | Frontier-quality open weights |
| **LLaMA 3.3 70B** | Dense | 128K | 70B | Excellent quality/size |
| **LLaMA 3.2 3B/1B** | Dense | 128K | 1–3B | Edge and on-device |
| **LLaMA 3.1 405B** | Dense | 128K | 405B | Closest to frontier among older releases |

**Ecosystem:** Most widely supported by every serving framework (vLLM, Ollama, llama.cpp, TGI, etc.)

---

### Alibaba — Qwen Family

Strong open-weight models, especially for multilingual (100+ languages) and coding.

| Model | Context | Notes |
|---|---|---|
| **Qwen 2.5-72B** | 128K | Excellent quality; strong multilingual |
| **Qwen 2.5-Coder-32B** | 32K | Top coding model in open category |
| **Qwen 2.5-VL-72B** | 32K | Vision + language multimodal |
| **QwQ-32B** | 128K | Reasoning/thinking model |

---

### DeepSeek

DeepSeek (China) created waves in early 2025 with frontier-quality models at dramatically lower training cost.

| Model | Type | Context | Notes |
|---|---|---|---|
| **DeepSeek-V3** | MoE (671B total, 37B active) | 128K | Near-frontier quality at 1/10 training cost of competitors |
| **DeepSeek-R1** | Reasoning | 128K | o1-class reasoning; fully open weights |
| **DeepSeek-R1-Distill** | Dense | 128K | Distilled to 1.5B–70B; high reasoning efficiency |

**Significance:** Demonstrated that frontier-quality models could be trained at dramatically lower compute budgets. R1 training methodology (GRPO + verifiable rewards) inspired industry-wide shifts.

---

### Microsoft — Phi Family (Small Language Models)

Phi models are designed for efficiency: frontier-quality reasoning in very small parameter counts.

| Model | Params | Context | Notes |
|---|---|---|---|
| **Phi-4** | 14B | 16K | Outperforms models 5× its size on reasoning benchmarks |
| **Phi-3.5-mini** | 3.8B | 128K | Mobile/edge deployment |
| **Phi-3-vision** | 4.2B | 128K | Multimodal at tiny scale |

---

### Google — Gemma Family (Open)

Google's open-weight models, distilled from Gemini.

| Model | Params | Notes |
|---|---|---|
| **Gemma 3 27B** | 27B | Best quality in Gemma family |
| **Gemma 3 12B** | 12B | Good balance; outperforms many 70B older models |
| **Gemma 3 4B/1B** | 4B/1B | On-device/edge |
| **CodeGemma** | 7B | Code generation |

---

## 1.3 Specialized Models

### Code Models

| Model | Provider | Notes |
|---|---|---|
| **DeepSeek-Coder-V2** | DeepSeek | Best open code model |
| **Codestral** | Mistral | Fast; FIM support for code completion |
| **Qwen 2.5-Coder** | Alibaba | Strong multilingual code |
| **StarCoder2** | HuggingFace/BigCode | Open; 619B token training |

### Reasoning Models

| Model | Provider | Notes |
|---|---|---|
| **o3** | OpenAI | Best overall reasoning |
| **o4-mini** | OpenAI | Fast + cheap reasoning |
| **Claude Opus** with extended thinking | Anthropic | Best for nuanced reasoning |
| **DeepSeek-R1** | DeepSeek | Open-weight; GRPO-trained |
| **QwQ-32B** | Alibaba | Open; strong reasoning |

### Embedding Models

Covered in depth in [Chapter 5](./05-embeddings-and-vector-tech.md).

| Model | Provider | Dims | Notes |
|---|---|---|---|
| **voyage-3-large** | Voyage AI | 1024 | Best retrieval quality |
| **text-embedding-3-large** | OpenAI | 3072 | Matryoshka support |
| **embed-v4.0** | Cohere | 1024 | Best price/quality |
| **bge-m3** | BAAI | 1024 | Best open-source multilingual |

### Multimodal Models

| Model | Modalities | Notes |
|---|---|---|
| **GPT-4o** | Text + Image + Audio | Best overall multimodal |
| **Gemini 2.5 Pro** | Text + Image + Video + Audio | Best video understanding |
| **Claude Sonnet/Opus** | Text + Image + PDF | Best document analysis |
| **Qwen 2.5-VL** | Text + Image | Best open multimodal |
| **LLaMA 4** | Text + Image | Open multimodal |

---

## 1.4 Provider Comparison by Use Case

| Use Case | Best Choice | Runner-Up | Why |
|---|---|---|---|
| Complex reasoning & analysis | Claude Opus 4.8 | o3 | Constitutional AI alignment; extended thinking |
| Coding | Grok 4 / Claude Sonnet | o4-mini | SWE-bench leadership |
| Long documents (>200K tokens) | Gemini 2.5 Pro | Claude Opus | 2M context window |
| High-volume / cost-sensitive | gpt-4o-mini / Gemini Flash | Claude Haiku | Lowest cost at quality floor |
| Self-hosting / privacy | LLaMA 4 Maverick | DeepSeek-V3 | Best open-weight quality |
| Multilingual | Gemini 2.5 / Qwen 2.5 | Claude | Stronger multilingual training data |
| Multimodal | Gemini 2.5 Pro | GPT-4o | Video + audio + image native |
| Reasoning (math/logic) | o3 / DeepSeek-R1 | Claude Opus with thinking | Dedicated reasoning training |
| European data residency | Mistral Large 2 | — | EU-based; GDPR-native |

---

## 1.5 Model Benchmarks Reference

Key benchmarks to evaluate LLMs (see full details in [Chapter 12](./12-key-papers-and-benchmarks.md)):

| Benchmark | Measures | Leader (June 2026) |
|---|---|---|
| **MMLU** | Broad knowledge (57 subjects) | GPT-5, Claude Opus |
| **HumanEval** | Python code generation | Grok 4, Claude Opus |
| **SWE-bench Verified** | Real GitHub issue resolution | Grok 4 (~75%) |
| **GPQA Diamond** | PhD-level science reasoning | Claude Mythos, Gemini 2.5 |
| **MATH** | Mathematical problem solving | o3, DeepSeek-R1 |
| **ARC-AGI-2** | Abstract reasoning | Gemini 3 Pro |
| **HLE** | Frontier science + math | Grok 4 (50.7%) |
| **MMMU** | Multimodal understanding | Gemini 2.5 Pro |

---

*[← Back to Bible Index](./README.md) | [Next: Architectures & Algorithms →](./02-architectures-and-algorithms.md)*

*Sources: [vellum.ai LLM Leaderboard](https://www.vellum.ai/llm-leaderboard) · [llm-stats.com](https://llm-stats.com/) · [artificialanalysis.ai](https://artificialanalysis.ai/leaderboards/models) · Provider official documentation*
