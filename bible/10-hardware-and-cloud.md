# Chapter 10 — Hardware & Cloud

> GPU architectures, cloud AI services, and infrastructure decisions for AI engineering.

---

## 10.1 GPU Reference

### NVIDIA GPU Lineup (AI/ML)

| GPU | VRAM | TF32 TFLOPs | HBM BW | Form Factor | Est. Price | Notes |
|---|---|---|---|---|---|---|
| **H200 SXM** | 141 GB | 989 | 4.8 TB/s | Data center | ~$40K | Best for 70B+ models |
| **H100 SXM** | 80 GB | 989 | 3.35 TB/s | Data center | ~$30K | Standard frontier |
| **H100 PCIe** | 80 GB | 756 | 2 TB/s | Server | ~$25K | Less NVLink BW |
| **A100 SXM 80GB** | 80 GB | 312 | 2 TB/s | Data center | ~$10K | Previous gen standard |
| **A100 PCIe 40GB** | 40 GB | 312 | 1.6 TB/s | Server | ~$8K | Budget A100 |
| **A10G** | 24 GB | 125 | 600 GB/s | Server/cloud | ~$3.5K | Cloud inference standard |
| **L40S** | 48 GB | 366 | 864 GB/s | Server | ~$12K | Inference-optimized |
| **RTX 4090** | 24 GB | 165 | 1.0 TB/s | Consumer | ~$1.5K | Best consumer for fine-tuning |
| **RTX 4080** | 16 GB | 97 | 717 GB/s | Consumer | ~$1.2K | Edge of QLoRA range |
| **RTX 3090** | 24 GB | 71 | 936 GB/s | Consumer | ~$800 | QLoRA on 13B |

**NVLink bandwidth:**
- H100 SXM: 900 GB/s NVLink (essential for tensor parallelism)
- H100 PCIe: 600 GB/s NVLink
- A100 SXM: 600 GB/s NVLink
- Consumer GPUs: PCIe only (no NVLink)

**Blackwell (2025):**
| GPU | VRAM | Notes |
|---|---|---|
| **B200** | 192 GB | Next-gen flagship |
| **GB200 NVL72** | 13.5 TB (72 GPUs) | System-level NVL rack |
| **RTX 5090** | 32 GB | Consumer; ~$2K |

---

### AMD GPU Lineup

| GPU | VRAM | FP16 TFLOPs | Notes |
|---|---|---|---|
| **MI300X** | 192 GB | 1.307 | Competitive with H100; ROCm |
| **MI250X** | 128 GB | 383 | Data center; popular in research |
| **RX 7900 XTX** | 24 GB | 123 | Consumer; ROCm supported |

**ROCm ecosystem:** Growing but narrower than CUDA. Most major frameworks (PyTorch, JAX) support it.

---

### Google TPUs

| TPU | HBM | Notes |
|---|---|---|
| **TPU v5p** | 95 GB/chip | Highest throughput for training |
| **TPU v5e** | 16 GB/chip | Cost-efficient inference |
| **TPU v4** | 32 GB/chip | Previous gen; widely available |

**Best for:** JAX/XLA workloads; Gemini training; GCP-native.

---

### Apple Silicon (On-Device)

| Chip | Unified Memory | Notes |
|---|---|---|
| **M4 Ultra** | Up to 192 GB | Best for on-device inference |
| **M4 Max** | Up to 128 GB | Pro workstation |
| **M4 Pro** | Up to 48 GB | MacBook Pro |
| **M4** | Up to 24 GB | MacBook Air; iPhone |

**What fits on Apple Silicon:**
- M4 Max (128GB): 70B model in Q4 with llama.cpp
- M4 Pro (48GB): 30B model in Q4
- M4 (24GB): 13B model in Q4

---

## 10.2 Cloud GPU Providers

### Major Cloud (GPU Instances)

| Provider | Instance | GPU | VRAM | Price/hr |
|---|---|---|---|---|
| **AWS** | p4d.24xlarge | 8× A100 40GB | 320 GB | ~$32 |
| **AWS** | p5.48xlarge | 8× H100 80GB | 640 GB | ~$98 |
| **GCP** | a3-highgpu-8g | 8× H100 80GB | 640 GB | ~$98 |
| **Azure** | ND H100 v5 | 8× H100 80GB | 640 GB | ~$98 |
| **AWS** | g5.xlarge | A10G | 24 GB | ~$1.0 |
| **GCP** | g2-standard-4 | L4 | 24 GB | ~$0.7 |

### Specialty GPU Clouds (Lower Cost)

| Provider | Hardware | Price | Notes |
|---|---|---|---|
| **Lambda Labs** | H100, A100 | $2–3/hr | Cheap H100s; less managed |
| **Vast.ai** | Various | $0.5–5/hr | Marketplace; cheapest |
| **RunPod** | H100, A100, RTX | $0.5–4/hr | Good DX; community |
| **CoreWeave** | H100, A100 | $2–4/hr | Acquired W&B; large fleet |
| **Together AI** | H100 | Pay-per-token | Managed inference + fine-tuning |
| **Fireworks AI** | H100 | Pay-per-token | Fast inference |
| **Lepton AI** | Various | Pay-per-use | Simple GPU APIs |

---

## 10.3 Cloud AI Services

### AWS

| Service | Description |
|---|---|
| **Amazon Bedrock** | Managed API for Claude, LLaMA, Titan, Mistral, Cohere |
| **SageMaker** | Full MLOps platform; training + serving |
| **SageMaker JumpStart** | Foundation model hub; one-click deploy |
| **Amazon Q** | Enterprise AI assistant |
| **Rekognition** | Computer vision API |
| **Transcribe** | Speech-to-text |
| **Comprehend** | NLP: entities, sentiment |
| **Kendra** | Enterprise semantic search |

### Google Cloud (GCP)

| Service | Description |
|---|---|
| **Vertex AI** | Full MLOps; model deployment; GenAI |
| **Vertex AI Gemini API** | Gemini model access |
| **Vertex AI Studio** | Prompting + fine-tuning UI |
| **Google AI Studio** | Free Gemini API playground |
| **Cloud Vision** | Computer vision API |
| **Cloud Speech** | Speech-to-text |
| **Natural Language AI** | NLP APIs |
| **Dialogflow** | Conversational AI |

### Microsoft Azure

| Service | Description |
|---|---|
| **Azure OpenAI** | GPT-4o, o3 with enterprise SLAs |
| **Azure AI Studio** | Full GenAI development platform |
| **Azure AI Search** | Cognitive search + RAG |
| **Azure ML** | MLOps platform |
| **Copilot Studio** | Low-code AI assistant builder |
| **Content Safety** | Content moderation API |
| **Azure AI Vision** | Computer vision |
| **Azure Speech** | Speech services |

---

## 10.4 Model Count by GPU (Reference)

| Model | BF16 | INT8 | INT4 AWQ | Minimum GPU |
|---|---|---|---|---|
| LLaMA 3 8B | 16 GB | 8 GB | 4 GB | RTX 4060 (8GB) with INT4 |
| LLaMA 3 70B | 140 GB | 70 GB | 35 GB | 2× A100 80GB |
| LLaMA 4 Maverick (100B active) | 200 GB | 100 GB | 50 GB | 4× A100 80GB |
| LLaMA 3.1 405B | 810 GB | 405 GB | 202 GB | 10× A100 80GB |
| Mixtral 8×7B (47B total) | 94 GB | 47 GB | 24 GB | A100 80GB + A100 40GB |

---

## 10.5 Cost Optimization on Cloud

| Optimization | Savings | Effort |
|---|---|---|
| **Spot/Preemptible instances** | 60–90% on training | Medium |
| **Reserved instances** | 30–60% on inference | Low |
| **Auto-scaling** | Pay only when active | Medium |
| **Mixed precision (BF16)** | 2× capacity vs FP32 | Low |
| **Quantization** | 2–4× capacity | Low–Medium |
| **Multi-tenant serving** | Amortize fixed cost | Medium |
| **Batch API** | 50% off async workloads | Low |

---

*[← Chapter 9: MLOps & Platforms](./09-mlops-and-platforms.md) | [Chapter 11: Security & Safety →](./11-security-and-safety.md)*
