# Chapter 4 — Inference & Serving

> Every tool, technique, and optimization for deploying and serving AI models in production.

---

## 4.1 Serving Frameworks

### vLLM (UC Berkeley, 2023)

The production standard for LLM serving. Key innovations: PagedAttention + continuous batching.

| Feature | Detail |
|---|---|
| **PagedAttention** | KV-cache managed like OS virtual memory; ~4× larger effective batch size |
| **Continuous batching** | New requests join mid-batch; GPU never idle |
| **OpenAI-compatible API** | Drop-in for OpenAI clients |
| **Quantization** | INT4 (AWQ/GPTQ), INT8, FP8 native |
| **Speculative decoding** | Draft model for 2–3× speedup |
| **Tensor/pipeline parallel** | Multi-GPU serving |
| **Prefix caching** | Reuse KV-cache for shared system prompts |

```bash
# Minimal production deployment
python -m vllm.entrypoints.openai.api_server \
    --model meta-llama/Llama-3-8B-Instruct \
    --gpu-memory-utilization 0.90 \
    --enable-prefix-caching
```

### SGLang (Stanford, 2024)

Optimized for complex multi-call workflows (agents, RAG, multi-turn).

| Feature | Detail |
|---|---|
| **RadixAttention** | KV-cache sharing via radix tree; better than vLLM for shared prefixes |
| **Speculative decoding** | Built-in |
| **Structured output** | JSON schema enforcement |
| **Continuous batching** | Similar to vLLM |

**Best for:** Agent workloads where many requests share long system prompts or document contexts.

### NVIDIA Triton Inference Server

Production standard for multi-model GPU platforms.

| Feature | Detail |
|---|---|
| **Multi-framework** | TensorFlow, PyTorch, ONNX, TensorRT, custom Python backends |
| **Concurrent models** | Multiple models on same GPU |
| **Dynamic batching** | Request batching with configurable delay |
| **gRPC + HTTP** | Both protocols supported |
| **Ensemble models** | Chain multiple models in a pipeline |

**Best for:** Organizations running LLMs alongside vision models, audio models, or custom ML.

### TensorRT-LLM (NVIDIA)

NVIDIA's LLM inference optimization library. Maximizes H100/A100 throughput.

| Feature | Detail |
|---|---|
| **CUDA kernels** | Custom high-performance kernels for LLM ops |
| **FP8 support** | Native H100 Tensor Core utilization |
| **In-flight batching** | Continuous batching like vLLM |
| **Multi-GPU** | Tensor + pipeline parallelism |

**Best for:** Maximum performance on NVIDIA hardware; integrates with Triton.

### Text Generation Inference — TGI (HuggingFace)

⚠️ **Maintenance mode since December 2025.** New deployments should use vLLM or SGLang.

| Feature | Detail |
|---|---|
| **Status** | Maintenance mode; no new features |
| **Migration** | vLLM is the recommended migration path |

### TorchServe (Meta/AWS)

PyTorch-native model serving for non-LLM PyTorch models.

| Feature | Detail |
|---|---|
| **Framework** | PyTorch native |
| **Use case** | Classification, regression, traditional ML |
| **Multi-model** | Load multiple models simultaneously |
| **LLM use** | Not optimized for LLMs; use vLLM instead |

### llama.cpp

CPU inference (and GPU offloading) via GGUF quantized models.

| Feature | Detail |
|---|---|
| **CPU inference** | Runs on any hardware including M-series Macs |
| **GGUF format** | Quantized model format (Q4_K_M, Q8_0, etc.) |
| **GPU offload** | Partially offload layers to GPU |
| **OpenAI API** | Optional OpenAI-compatible server |

### Ollama

Developer-friendly wrapper around llama.cpp.

| Feature | Detail |
|---|---|
| **One command** | `ollama run llama3` downloads and runs |
| **Model library** | 100+ models available |
| **API** | OpenAI-compatible REST API |
| **Best for** | Local development; not production-grade |

---

## 4.2 Quantization Reference

### Precision Formats

| Format | Bits | Memory (7B) | Quality Loss | Notes |
|---|---|---|---|---|
| FP32 | 32 | 28 GB | None (reference) | Training; not inference |
| BF16 | 16 | 14 GB | Negligible | Standard inference |
| FP16 | 16 | 14 GB | Negligible | Older; BF16 preferred |
| FP8 | 8 | 7 GB | <0.5% | H100/H200 hardware; production-ready |
| INT8 | 8 | 7 GB | <1% | LLM.int8(); production-ready |
| INT4 (AWQ) | 4 | 3.5 GB | 1–2% | Best INT4 method; vLLM native |
| INT4 (GPTQ) | 4 | 3.5 GB | 1–3% | Better on real-world tasks vs AWQ |
| NF4 (bitsandbytes) | 4 | 3.5 GB | 1–2% | Used in QLoRA training |
| GGUF Q4_K_M | 4 | ~4 GB | 2–3% | llama.cpp; CPU inference |
| INT2 | 2 | 1.75 GB | 5–15% | Extreme compression; quality degraded |

### Methods

| Method | Algorithm | Key Feature |
|---|---|---|
| **LLM.int8()** | Mixed-precision; keep outliers in FP16 | Handles emergent outliers |
| **GPTQ** | Layer-wise quantization minimizing output error | Post-training; calibration data needed |
| **AWQ** | Protect salient 1% of weights by scaling | Activation-aware; currently standard |
| **FP8** | Native hardware format (H100+) | Best accuracy at 8-bit |
| **GGUF/GGML** | CPU-friendly format; k-quants | llama.cpp; on-device |
| **SpQR** | 2-bit base + outliers in higher precision | Research frontier |
| **SqueezeLLM** | Non-uniform quantization | Research |

---

## 4.3 Parallelism Strategies

| Strategy | Split | Latency | Throughput | Interconnect |
|---|---|---|---|---|
| **Tensor Parallelism (TP)** | Each layer across GPUs | Best (all GPUs per token) | Good | Requires NVLink |
| **Pipeline Parallelism (PP)** | Layers across GPUs | Higher (sequential layers) | Best | PCIe OK |
| **Data Parallelism (DP)** | Full model replicated | Same as single GPU | Best (multiple instances) | Any |
| **Expert Parallelism** | MoE experts across GPUs | Good | Good | Any |

**Practical guide:**
- Single node, model too large for 1 GPU → TP within node (NVLink needed for efficiency)
- Multi-node, extreme scale → PP across nodes + TP within node
- Model fits, need throughput → DP (simplest, most efficient)

---

## 4.4 Key Serving Optimizations

### Speculative Decoding
- Draft model proposes N tokens (fast)
- Target model verifies all N in parallel (1 forward pass)
- Accept matched tokens; reject remainder
- **Result:** 2–3× speedup with identical output quality

### KV-Cache Optimization

| Technique | Memory Saved | Quality Impact |
|---|---|---|
| **Prefix caching** | Reuse KV for shared prefix | None |
| **KV quantization (FP8)** | ~50% KV cache memory | <0.5% |
| **PagedAttention** | Eliminates fragmentation waste | None |
| **KV cache eviction** | Remove low-attention tokens | Slight |
| **Cross-request KV sharing** | SGLang RadixAttention | None |

### Flash Attention
- Reorders attention computation to use GPU SRAM instead of HBM
- Memory: O(n²) → O(n)
- Speed: 2–4× faster than standard attention
- **Flash Attention 3** (2024): 1.5–2× faster than FA2 on H100

---

## 4.5 Deployment Patterns

| Pattern | Description | Use When |
|---|---|---|
| **Single model** | One model behind load balancer | Simple; most common |
| **Blue-green** | Two versions; shift traffic gradually | Zero-downtime updates |
| **Canary** | 5% new version, monitor, then full rollout | Risk-averse production |
| **Shadow** | New version gets copy of traffic but responses hidden | Testing without user impact |
| **A/B split** | Two versions, measure quality difference | Optimization experiments |
| **Model routing** | Route by query type to appropriate model | Cost optimization |
| **Disaggregated prefill** | Separate prefill (compute-bound) from decode (memory-bound) | Frontier efficiency 2026 |

---

*[← Chapter 3: Training Techniques](./03-training-techniques.md) | [Chapter 5: Embeddings & Vector Tech →](./05-embeddings-and-vector-tech.md)*
