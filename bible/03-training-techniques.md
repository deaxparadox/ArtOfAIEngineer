# Chapter 3 — Training Techniques

> Every method used to train, align, and adapt language models — from pre-training to RLVR.

---

## 3.1 Pre-Training

The first phase of LLM development. Train on massive text corpora using next-token prediction.

### Objectives

| Objective | How | Models |
|---|---|---|
| **Causal LM (CLM)** | Predict next token; left-to-right | GPT, LLaMA, Claude, all decoder-only |
| **Masked LM (MLM)** | Predict masked tokens; bidirectional | BERT, RoBERTa |
| **Span corruption** | Predict masked spans | T5 |
| **Prefix LM** | Some tokens causal, some bidirectional | UL2, GLM |

### Data Sources and Filtering

| Source | Typical % | Notes |
|---|---|---|
| Common Crawl | 50–60% | Must be heavily filtered (~1–5% survives) |
| Books | 10–20% | Long-form coherence |
| Wikipedia | 3–5% | Factual grounding |
| Code (GitHub) | 10–15% | Enables coding ability |
| Academic papers | 3–5% | ArXiv, PubMed, Semantic Scholar |
| Curated sources | Varies | C4, FineWeb, RedPajama, DCLM |

**Quality datasets (2024–2026):**
- **FineWeb** (HuggingFace): High-quality CC subset; better than raw CC
- **DCLM** (DataComp LM): Systematic quality evaluation framework
- **RedPajama v2**: Open replication of LLaMA training data
- **Dolma** (AI2): Used for OLMo; fully open

### Distributed Training Strategies

| Strategy | What It Does | Use When |
|---|---|---|
| **Data Parallelism (DP)** | Same model on N GPUs, different batches | Model fits on 1 GPU |
| **Tensor Parallelism (TP)** | Split each layer across GPUs (intra-layer) | Large models; requires NVLink |
| **Pipeline Parallelism (PP)** | Assign layers to different GPUs (inter-layer) | Very large models; inter-node |
| **FSDP** | Shard model weights + gradients | Memory-efficient DP; PyTorch native |
| **ZeRO** (DeepSpeed) | Shard optimizer states / gradients / params | Large model training without model parallel |
| **3D Parallelism** | TP + PP + DP combined | Megatron-scale training |

### Training Frameworks

| Framework | Creator | Notes |
|---|---|---|
| **Megatron-LM** | NVIDIA | Industry standard for large-scale LLM training |
| **DeepSpeed** | Microsoft | ZeRO; used widely with Megatron |
| **FSDP** | PyTorch/Meta | Native PyTorch distributed training |
| **JAX/XLA** | Google | Used for Gemini training; TPU-optimized |
| **torchtitan** | Meta | New PyTorch-native LLM training framework (2024) |
| **litgpt** | Lightning AI | Clean hackable LLM training |

---

## 3.2 Post-Training / Alignment Pipeline

The modern alignment pipeline for production models (2026 standard):

```
Pre-trained base model
        ↓
Supervised Fine-Tuning (SFT)
        ↓
Preference Optimization (DPO or RLHF)
        ↓ (for reasoning models only)
RLVR (verifiable reward training)
        ↓
Aligned production model
```

---

## 3.3 Supervised Fine-Tuning (SFT)

Train the base model on curated (instruction, response) pairs.

### Data Format

```json
// Standard chat format
{
  "messages": [
    {"role": "system", "content": "You are a helpful assistant."},
    {"role": "user", "content": "What is Python?"},
    {"role": "assistant", "content": "Python is a high-level programming language..."}
  ]
}
```

### Critical Concepts

**Loss masking:** Only compute loss on assistant tokens. Prompt tokens are masked (label=-100).
Without loss masking: model learns to predict prompts. With loss masking: model learns to respond.

**Chat templates:** Each model family has specific formatting (LLaMA-3, ChatML, Mistral).
Always use `tokenizer.apply_chat_template()` — never format manually.

### SFT Libraries

| Library | Notes |
|---|---|
| **TRL (HuggingFace)** | `SFTTrainer`; handles masking, templating automatically |
| **Axolotl** | Config-driven; production-grade; best defaults |
| **LLaMAFactory** | Web UI + CLI; easy for beginners |
| **torchtune** | Meta's official tool; pure PyTorch |
| **Unsloth** | 2–4× faster training via custom kernels |

---

## 3.4 RLHF — Reinforcement Learning from Human Feedback

**Three-stage pipeline:**
1. **SFT:** Train on human demonstrations
2. **Reward model:** Train RM to predict human preferences (Bradley-Terry loss on preference pairs)
3. **RL with PPO:** Optimize LLM using RM as reward signal; KL constraint to prevent reward hacking

**Challenge:** PPO is notoriously unstable. Complex to tune. Reward hacking (model games the RM).
**Status 2026:** Largely replaced by DPO for most organizations. Still used for online RLHF at top labs.

---

## 3.5 DPO — Direct Preference Optimization

Skips the separate reward model. Directly optimizes from preference pairs using a reformulated objective.

**Data format:** `(prompt, chosen_response, rejected_response)` triplets

**Loss:**
```
L_DPO = -E[log σ(β · log(π(y_w|x)/π_ref(y_w|x)) - β · log(π(y_l|x)/π_ref(y_l|x)))]
```

**Variants:**

| Method | Key Difference | Notes |
|---|---|---|
| **DPO** | Original | Stable; default choice |
| **IPO** | Identity preference | More conservative |
| **ORPO** | Online + reference-free | Combines SFT+DPO in one step |
| **SimPO** | No reference model | Simpler; margin reward |
| **RLOO** | Multi-sample rollout | More sample-efficient |
| **β-DPO** | Dynamic β | Better calibration |
| **Contrastive DPO** | Hard negatives | Better rejection |

**Status 2026:** DPO is the default post-training alignment method. Most open-source instruction-tuned models use SFT → DPO.

---

## 3.6 RLVR — Reinforcement Learning with Verifiable Rewards

Training on tasks with verifiable answers (math, code with tests) as reward signal. No human annotation needed.

**Process:**
```
For each problem:
  1. Model generates candidate solution
  2. Verify answer (run code, check math, validate format)
  3. Reward = 1 if correct, 0 if wrong
  4. Update model via GRPO/PPO to increase correct answers
```

**GRPO (Group Relative Policy Optimization):**
- Generate N responses per prompt
- Rank them by verifiable reward
- Update model to increase probability of higher-ranked responses
- No separate critic/baseline model needed

**Examples:**
- DeepSeek-R1: Trained with GRPO on math + code → strong reasoning
- OpenAI o1/o3: RLVR on math, coding, science
- Claude 3.7 Sonnet: Extended thinking trained with similar methods

**Why it works:** Verifiable signals are noise-free (correct/incorrect is objective). Self-generates training data. Scales without human annotation.

---

## 3.7 Constitutional AI (CAI) — Anthropic's Approach

Two-stage alignment that scales human feedback via AI feedback:

**Stage 1 (SL-CAI):** Supervised learning with self-critique
1. Generate responses
2. Have model critique its own responses against a "constitution" of principles
3. Revise responses
4. Fine-tune on revised responses

**Stage 2 (RL-CAI):** Reinforcement learning from AI feedback
- Use a larger model to score responses against the constitution
- Train a reward model from AI preferences
- Apply PPO with AI-generated reward signal

**Result:** Scales preference labeling without human annotators for every example. Used in Claude training.

---

## 3.8 Parameter-Efficient Fine-Tuning (PEFT)

Adapt large models by training only a small fraction of parameters.

### LoRA — Low-Rank Adaptation

Decompose weight update ΔW into two low-rank matrices: `ΔW ≈ B × A` where rank r << d.

```python
# r=16 for 7B model: trains 83M/7B = ~1.2% of parameters
# Quality: ~98% of full fine-tuning quality
```

| Parameter | Range | Effect |
|---|---|---|
| `r` (rank) | 4–128 | Higher = more capacity; start at 16 |
| `lora_alpha` | Usually 2r | Scaling factor |
| `target_modules` | q/k/v/o projections | Which layers to adapt |
| `lora_dropout` | 0.0–0.1 | Regularization |

**Inference overhead:** Zero after merging LoRA into base weights.

### QLoRA — Quantized LoRA

Load base model in 4-bit (NF4 quantization), train LoRA adapters in full precision.

| Resource | Full FT (7B) | LoRA | QLoRA |
|---|---|---|---|
| GPU VRAM | ~66 GB | ~18 GB | ~10 GB |
| Training speed | Slowest | Moderate | Moderate |
| Quality | 100% | ~98% | ~95% |
| Hardware needed | A100 80GB × 2 | A100 40GB | RTX 4090 (24GB) |

### Other PEFT Methods

| Method | Approach | Notes |
|---|---|---|
| **Adapters** | Small FFN layers inserted between transformer layers | Modular; can have multiple adapters |
| **Prefix tuning** | Learnable "soft prompts" prepended to input | No parameter increase at serving |
| **IA³** | Scale existing activations; few parameters | Minimal interference |
| **DoRA** | Decompose into magnitude + direction components | Sometimes better than LoRA |
| **GaLore** | Gradient low-rank projection | Memory-efficient pre-training |

---

## 3.9 Knowledge Distillation

Transfer knowledge from a large "teacher" model to a smaller "student" model.

| Method | Teacher Signal | Notes |
|---|---|---|
| **Hard-label KD** | Teacher's predicted class | Simple; original KD |
| **Soft-label KD** | Teacher's probability distribution | Better; captures uncertainty |
| **Feature KD** | Intermediate layer representations | More knowledge transferred |
| **SeqKD** | Teacher-generated text data | Simple; works for LLMs |
| **On-policy distillation** | Student rollouts scored by teacher | Used for small reasoning models |

**LLM distillation examples:**
- Llama 3.2 1B/3B: Distilled from Llama 3.1 70B/405B
- DeepSeek-R1-Distill: R1's reasoning distilled into 1.5B–70B dense models
- Phi-4: Very small model; frontier reasoning from distillation

---

## 3.10 Continual Learning / Domain Adaptation

Training a pre-trained model on new domain data without forgetting general capabilities.

| Method | Technique | Forgetting Risk |
|---|---|---|
| **Continued pre-training** | Keep pre-training on domain corpus | Medium |
| **Replay buffers** | Mix new + old data | Low |
| **EWC** (Elastic Weight Consolidation) | Penalize changes to important weights | Low |
| **LoRA for domain** | Only LoRA adapters update | Very low (base frozen) |

---

*[← Chapter 2: Architectures & Algorithms](./02-architectures-and-algorithms.md) | [Chapter 4: Inference & Serving →](./04-inference-and-serving.md)*
