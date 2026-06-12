# Chapter 12 — Key Papers & Benchmarks

> The canon papers every AI engineer should know, and the benchmarks used to measure progress.

---

## 12.1 Foundational Papers (Must-Read)

### Architecture

| Paper | Year | Key Contribution |
|---|---|---|
| **Attention Is All You Need** — Vaswani et al. | 2017 | Transformer architecture; replaces RNNs |
| **BERT** — Devlin et al. | 2018 | Bidirectional pre-training; NLP encoder-only |
| **GPT-2** — Radford et al. | 2019 | Language modeling at scale; generation |
| **GPT-3** — Brown et al. | 2020 | Few-shot learning; scale unlocks capability |
| **Scaling Laws** — Kaplan et al. | 2020 | Predictable power-law scaling |
| **Chinchilla** — Hoffmann et al. | 2022 | Compute-optimal training; data > params |
| **Emergent Abilities of LLMs** — Wei et al. | 2022 | Capabilities appear suddenly at scale |

### Alignment

| Paper | Year | Key Contribution |
|---|---|---|
| **InstructGPT** — Ouyang et al. | 2022 | RLHF for instruction following |
| **Constitutional AI** — Bai et al. | 2022 | Anthropic's CAI approach |
| **DPO** — Rafailov et al. | 2023 | Reward-model-free preference optimization |
| **RLHF paper** — Stiennon et al. | 2020 | Original RLHF for summarization |

### Efficient Fine-Tuning

| Paper | Year | Key Contribution |
|---|---|---|
| **LoRA** — Hu et al. | 2021 | Low-rank adaptation; parameter-efficient FT |
| **QLoRA** — Dettmers et al. | 2023 | 4-bit quantization + LoRA |
| **Adapter** — Houlsby et al. | 2019 | Small trainable modules |
| **Prefix Tuning** — Li & Liang | 2021 | Learnable soft prompts |

### RAG & Retrieval

| Paper | Year | Key Contribution |
|---|---|---|
| **RAG** — Lewis et al. | 2020 | Original RAG paper |
| **RETRO** — Borgeaud et al. | 2022 | Retrieval-enhanced transformer |
| **REALM** — Guu et al. | 2020 | Pre-training with retrieval |
| **HyDE** — Gao et al. | 2022 | Hypothetical document embeddings |

### Attention & Efficiency

| Paper | Year | Key Contribution |
|---|---|---|
| **Flash Attention** — Dao et al. | 2022 | IO-aware exact attention; O(n) memory |
| **Flash Attention 2** — Dao | 2023 | 2× speedup over FA1 |
| **Rotary Embeddings (RoPE)** — Su et al. | 2021 | Better positional encoding for long context |
| **ALiBi** — Press et al. | 2021 | Attention with linear biases |
| **Longformer** — Beltagy et al. | 2020 | Local + global attention for long docs |
| **Mamba** — Gu & Dao | 2023 | Selective state space model |

### Multimodal

| Paper | Year | Key Contribution |
|---|---|---|
| **CLIP** — Radford et al. | 2021 | Contrastive text-image pre-training |
| **DALL-E** — Ramesh et al. | 2021 | Text-to-image generation |
| **Flamingo** — Alayrac et al. | 2022 | Few-shot multimodal model |
| **LLaVA** — Liu et al. | 2023 | Visual instruction tuning |
| **GPT-4V** — OpenAI | 2023 | GPT-4 with vision |

### Prompting

| Paper | Year | Key Contribution |
|---|---|---|
| **Chain-of-Thought** — Wei et al. | 2022 | Step-by-step reasoning improves accuracy |
| **Self-Consistency** — Wang et al. | 2022 | Sample N chains; majority vote |
| **ReAct** — Yao et al. | 2022 | Reasoning + acting interleaved |
| **Tree of Thoughts** — Yao et al. | 2023 | Tree search over reasoning steps |
| **DSPy** — Khattab et al. | 2023 | Programming language model prompts |
| **Reflexion** — Shinn et al. | 2023 | Agent self-reflection and retry |

### Reasoning Models

| Paper | Year | Key Contribution |
|---|---|---|
| **DeepSeek-R1** — DeepSeek | 2025 | RLVR + GRPO for open reasoning models |
| **RLVR** (various) | 2024–2025 | Verifiable reward training for math/code |
| **QwQ** — Alibaba | 2024 | Open reasoning model |
| **Speculative Decoding** — Leviathan et al. | 2022 | Draft-verify paradigm |

---

## 12.2 Benchmarks Reference

### Language & Knowledge

| Benchmark | What It Tests | Baseline (random) | State of the Art |
|---|---|---|---|
| **MMLU** | 57 subjects; broad knowledge | 25% | ~90%+ (frontier) |
| **HellaSwag** | Commonsense reasoning | 25% | ~95%+ |
| **WinoGrande** | Commonsense (Winograd schema) | 50% | ~90%+ |
| **ARC-Challenge** | Grade-school science | 25% | ~92%+ |
| **TruthfulQA** | Truthfulness; avoiding falsehoods | ~25% | ~90% (frontier) |
| **BoolQ** | Boolean Q&A | 62% | ~90%+ |
| **LAMBADA** | Word prediction in context | — | ~88%+ |

### Reasoning

| Benchmark | What It Tests | State of the Art |
|---|---|---|
| **GSM8K** | Grade school math | ~99% (frontier + CoT) |
| **MATH** | Competition math | ~90%+ (frontier) |
| **GPQA Diamond** | PhD-level science | ~94% (Claude Mythos) |
| **ARC-AGI-2** | Abstract reasoning; pattern completion | ~60%+ (GPT-4o) |
| **HLE** (Humanity's Last Exam) | Frontier scientific reasoning | ~50% (Grok 4) |
| **BBH** (Big-Bench Hard) | 23 hard reasoning tasks | ~90%+ (frontier) |

### Coding

| Benchmark | What It Tests | State of the Art |
|---|---|---|
| **HumanEval** | Python function generation | ~99% (frontier) |
| **MBPP** | Python programming problems | ~98% (frontier) |
| **SWE-bench Verified** | Real GitHub issues | ~75% (Grok 4, GPT-5) |
| **SWE-bench Lite** | 300 curated GitHub issues | ~85%+ (frontier) |
| **LiveCodeBench** | Contamination-free coding | ~70%+ (frontier) |
| **BigCodeBench** | Complex function synthesis | ~80%+ (frontier) |

### Multimodal

| Benchmark | What It Tests | State of the Art |
|---|---|---|
| **MMMU** | College-level multimodal | ~80%+ (Gemini 2.5) |
| **MMBench** | Multimodal perception | ~90%+ |
| **VQAv2** | Visual question answering | ~85%+ |
| **TextVQA** | Text in images | ~90%+ |
| **DocVQA** | Document understanding | ~95%+ |
| **ChartQA** | Chart interpretation | ~90%+ |

### Safety & Alignment

| Benchmark | What It Tests |
|---|---|
| **TruthfulQA** | Avoiding falsehoods and hallucinations |
| **ToxiGen** | Hate speech and stereotypes |
| **BBQ** | Bias in ambiguous contexts |
| **HarmBench** | Comprehensive harmful behaviors |
| **StrongREJECT** | Robust jailbreak resistance |

### RAG & Retrieval

| Benchmark | What It Tests |
|---|---|
| **BEIR** | 18 retrieval datasets; zero-shot |
| **MTEB** | 58 embedding tasks across 8 categories |
| **RAGAS benchmarks** | RAG pipeline quality |
| **RGB** | RAG benchmark for generation |

---

## 12.3 Benchmark Caveats

1. **Data contamination:** Models may have been trained on benchmark data. Recent benchmarks (LiveCodeBench, HLE) specifically avoid this.

2. **Prompt sensitivity:** Small prompt changes can shift scores ±5%. Compare models using identical prompting.

3. **Benchmark saturation:** MMLU is nearly saturated (90%+ for frontier models). HLE, GPQA Diamond are the discriminating benchmarks as of 2026.

4. **Task-specific vs general:** A model that leads on MMLU may not lead on your specific task. Always evaluate on your own data.

5. **Leaderboard games:** Models can be fine-tuned specifically for benchmark performance without improving real-world quality.

---

*[← Chapter 11: Security & Safety](./11-security-and-safety.md) | [Chapter 13: Complete Tool Catalog →](./13-complete-tool-catalog.md)*
