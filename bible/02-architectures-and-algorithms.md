# Chapter 2 — Architectures & Algorithms

> Every major neural architecture, algorithm, and mathematical concept used in AI engineering — what it is, how it works, and when it's used.

---

## 2.1 Core Neural Architectures

### Transformer (2017 — Vaswani et al.)

The architecture that powers all modern LLMs. "Attention Is All You Need."

**Core components:**
- **Multi-head self-attention:** Each token attends to all other tokens simultaneously. O(n²) complexity.
- **Feed-forward network (FFN):** 2-layer MLP applied independently to each token. d_model → 4×d_model → d_model.
- **Layer normalization:** Applied before each sublayer (pre-norm in modern models).
- **Residual connections:** Skip connections around every sublayer.
- **Positional encoding:** Injects position information (sinusoidal original; RoPE/ALiBi in modern models).

**Variants:**
| Variant | Description | Examples |
|---|---|---|
| **Encoder-only** | Bidirectional; no generation | BERT, RoBERTa, DeBERTa |
| **Decoder-only** | Causal (left-to-right); generation | GPT, Claude, LLaMA |
| **Encoder-decoder** | Full bidirectional encoder + causal decoder | T5, BART, mT5 |

---

### Attention Mechanism

The core operation: `Attention(Q, K, V) = softmax(QKᵀ/√d_k) · V`

**Types:**
| Type | Description | Used In |
|---|---|---|
| **Self-attention** | Q, K, V all from same sequence | All transformers |
| **Cross-attention** | Q from decoder, K/V from encoder | Encoder-decoder models |
| **Multi-head attention (MHA)** | N parallel attention heads | Standard |
| **Grouped query attention (GQA)** | Multiple Q heads share K/V heads | LLaMA 3, Mistral (inference efficiency) |
| **Multi-query attention (MQA)** | All Q heads share single K/V | Falcon (extreme efficiency) |
| **Flash Attention** | Reordered I/O: same result, O(n) memory | All modern LLMs in training |
| **Sliding window / Longformer** | Each token attends to local window | Long documents |
| **Sparse attention** | Attend to subset of tokens | BigBird |
| **Linear attention** | O(n) approximation | Efficiency research |

---

### Mixture of Experts (MoE)

Instead of dense FFN layers, MoE uses N "expert" FFNs with a router that selects K for each token.

```
Standard FFN:        token → FFN (all 7B params active) → output
MoE (8 experts, top-2): token → Router → Expert 2, Expert 7 → output
                         8 experts × 1B params = 8B total, 2B active per token
```

**Why MoE:** More total capacity (knowledge) at same inference cost. Training requires all experts on GPU; inference only loads active experts.

**Examples:** Mixtral 8×7B, LLaMA 4, DeepSeek-V3 (671B total / 37B active), GPT-4 (estimated), Grok (estimated)

---

### Convolutional Neural Networks (CNNs)

Spatial feature extractors. Used for images, audio spectrograms, and 1D sequences.

| Layer Type | What It Does |
|---|---|
| **Conv2D** | Applies learned filters; detects local patterns |
| **Pooling (Max/Avg)** | Spatial downsampling; translation invariance |
| **Residual connection** | Skip connections for deep networks (ResNet) |
| **Batch normalization** | Normalizes layer inputs; accelerates training |
| **Depthwise separable conv** | Efficient factored convolution (MobileNet) |

**Key architectures:**
- **ResNet** (2015): Residual connections enabled 100+ layer training
- **EfficientNet** (2019): Compound scaling; best accuracy/compute
- **ConvNeXt** (2022): CNN redesigned with transformer principles
- **Vision Transformer (ViT)** (2020): Patches of image as tokens → transformer

---

### Recurrent Neural Networks (RNNs)

Sequential processing with hidden state. Largely replaced by transformers for NLP.

| Architecture | Key Feature | Status |
|---|---|---|
| **Vanilla RNN** | h_t = tanh(W_h·h_{t-1} + W_x·x_t) | Mostly obsolete |
| **LSTM** (1997) | Cell state + 3 gates (forget, input, output) | Still used for time series |
| **GRU** (2014) | Simplified LSTM (2 gates) | Time series, streaming |
| **Bidirectional RNN** | Processes sequence in both directions | NLP classification (pre-BERT era) |

**2026 status:** RNNs/LSTMs still used for time series forecasting and streaming (edge inference). Replaced by transformers for NLP.

---

### State Space Models (SSMs)

New class (2022–2024) competing with transformers for sequence modeling. O(n) inference.

| Model | Year | Key Innovation |
|---|---|---|
| **S4** | 2022 | First practical SSM for long sequences |
| **Mamba** | 2023 | Selective SSM; context-dependent state updates |
| **Mamba-2** | 2024 | Improved; competitive with transformers on some tasks |
| **RWKV** | 2023 | RNN-transformer hybrid; linear attention |
| **RetNet** | 2023 | Microsoft; retention mechanism |
| **Jamba** | 2024 | AI21; transformer + Mamba hybrid |

**2026 status:** SSMs are serious research frontier but haven't dethroned transformers at scale. Hybrid architectures (transformer + SSM layers) are emerging.

---

## 2.2 Training Algorithms

### Backpropagation & Gradient Descent

The fundamental optimization algorithm for all neural networks.

```
Forward pass:  compute loss L from weights W and data X
Backward pass: compute ∂L/∂W via chain rule
Update:        W ← W - η · ∂L/∂W
```

| Optimizer | Key Feature | When to Use |
|---|---|---|
| **SGD** | Stochastic gradient with optional momentum | CNNs, vision; careful tuning needed |
| **Adam** | Adaptive learning rates; momentum + RMSProp | Default; fast convergence |
| **AdamW** | Adam + decoupled weight decay | LLM training; standard since 2019 |
| **Adafactor** | Memory-efficient Adam | Large model training (T5 original) |
| **Lion** | Sign-based; 3× less memory than Adam | Large-scale vision/language |
| **Muon** | Nesterov + orthogonalization | Research frontier 2024–2025 |
| **GRPO** | Group Relative Policy Optimization | RLVR / reasoning model training |

---

### Learning Rate Schedules

| Schedule | Formula | Best For |
|---|---|---|
| **Constant** | η = η₀ | Baselines |
| **Step decay** | η × 0.1 every N epochs | Classical training |
| **Cosine annealing** | η = η_min + ½(η_max−η_min)(1 + cos(πt/T)) | LLM fine-tuning |
| **Linear warmup + cosine** | Ramp up then cosine decay | LLM pre-training (GPT, BERT) |
| **Warmup + constant + decay** | WSD (Weight, Stable, Decay) | Modern LLM training |
| **ReduceLROnPlateau** | Reduce when val loss stagnates | General use |

---

## 2.3 Positional Encodings

How transformers encode token position:

| Method | How It Works | Used In |
|---|---|---|
| **Sinusoidal** (original) | sin/cos at different frequencies | Original Transformer, BERT |
| **Learned absolute** | Trainable embedding per position | GPT-2, early models |
| **RoPE** (Rotary) | Rotate Q/K by position-dependent angle | LLaMA, Mistral, Qwen |
| **ALiBi** | Adds linear bias to attention scores | MPT, Falcon |
| **NoPE** (no positional encoding) | Some modern models skip explicit PE | LLaMA 4 experiments |

**Why RoPE dominates:** Generalizes better to longer contexts than trained on (with YaRN/LongRoPE extensions). Now standard in almost all new open-weight models.

---

## 2.4 Normalization Techniques

| Method | Normalizes Over | Used In |
|---|---|---|
| **BatchNorm** | Batch dimension | CNNs; problematic with variable batch sizes |
| **LayerNorm** | Feature dimension (per token) | Transformers (standard) |
| **RMSNorm** | RMS of features; no mean subtraction | LLaMA family; faster than LayerNorm |
| **GroupNorm** | Groups of features | When batch size is 1 |
| **Pre-norm** | Apply norm before sublayer | Modern LLMs (more stable) |
| **Post-norm** | Apply norm after sublayer + residual | Original transformer; less stable |

---

## 2.5 Activation Functions

| Function | Formula | Where Used |
|---|---|---|
| **ReLU** | max(0, x) | CNNs, MLPs |
| **Leaky ReLU** | max(αx, x) | Fixes dying ReLU |
| **GELU** | x·Φ(x) smooth approximation | BERT, GPT-2/3, most transformers |
| **SiLU / Swish** | x · sigmoid(x) | LLaMA FFN |
| **SwiGLU** | Swish(xW₁) ⊙ xW₂ | LLaMA 2+, PaLM, many modern LLMs |
| **GeGLU** | GELU(xW₁) ⊙ xW₂ | T5 variants |
| **Sigmoid** | 1/(1+e^{-x}) | Binary outputs, gates |
| **Softmax** | e^{x_i}/Σe^{x_j} | Attention weights, output probabilities |
| **Tanh** | (e^x - e^{-x})/(e^x + e^{-x}) | RNNs, some output layers |

---

## 2.6 Loss Functions

| Loss Function | Formula | Task |
|---|---|---|
| **Cross-entropy** | -Σ y·log(ŷ) | Classification, LLM training |
| **Binary cross-entropy** | -(y·log(ŷ) + (1-y)·log(1-ŷ)) | Binary classification |
| **MSE** | (1/n)Σ(y-ŷ)² | Regression |
| **MAE** | (1/n)Σ|y-ŷ| | Regression (outlier-robust) |
| **Huber loss** | Blend of MSE + MAE | Robust regression |
| **KL divergence** | Σ P·log(P/Q) | VAEs, distribution matching |
| **Contrastive loss** | Pull similar, push dissimilar | Embedding training |
| **NT-Xent** (SimCLR) | Contrastive with temperature | Self-supervised vision |
| **Bradley-Terry** | log σ(r_w - r_l) | Reward model training (RLHF) |
| **DPO loss** | -E[log σ(β·log π(y_w)/π_ref(y_w) - β·...)] | Direct preference optimization |

---

## 2.7 Regularization Techniques

| Technique | What It Does | When to Use |
|---|---|---|
| **L1 (Lasso)** | Penalty on Σ|w|; sparsity | Feature selection |
| **L2 / Weight decay** | Penalty on Σw²; small weights | Neural networks (default) |
| **Dropout** | Random zero-out during training | Fully-connected layers |
| **VariationalDropout** | Learned dropout per unit | Recurrent networks |
| **Stochastic depth** | Randomly skip layers | Deep ResNets |
| **Label smoothing** | Soft target labels (0.1 not 0.0) | Prevents overconfident predictions |
| **Early stopping** | Stop when val loss increases | Always |
| **Data augmentation** | Expand training set artificially | Images, text, audio |
| **Gradient clipping** | Cap gradient norm | Transformers (clip to 1.0 standard) |

---

## 2.8 Sampling / Decoding Strategies

How LLMs generate text from probability distributions:

| Strategy | Description | Temperature | Use When |
|---|---|---|---|
| **Greedy** | Always pick highest-probability token | 0 | Deterministic; factual Q&A |
| **Temperature sampling** | Divide logits by T before softmax | 0.7–1.0 | Creative generation |
| **Top-k** | Sample from top-k tokens | Any | Prevent tail sampling |
| **Top-p (nucleus)** | Sample from smallest set with prob ≥ p | Any | More natural than top-k |
| **Min-p** | Sample tokens with prob ≥ min_p × max_prob | Any | 2024 improvement over top-p |
| **Beam search** | Keep K best partial sequences | 0 | Translation, structured output |
| **Speculative decoding** | Draft model proposes N tokens; target verifies | Any | 2–3× latency improvement |
| **Contrastive decoding** | Use amateur model to avoid | Any | Reduce hallucination |

---

## 2.9 Tokenization Algorithms

| Method | How It Works | Used By |
|---|---|---|
| **BPE** (Byte Pair Encoding) | Merge most frequent character pairs iteratively | GPT-2/3/4, LLaMA |
| **Byte-level BPE** | BPE on raw bytes; no unknown tokens | GPT-2+, LLaMA 3 |
| **WordPiece** | Like BPE but uses likelihood | BERT, DistilBERT |
| **Unigram LM** | Top-down: prune vocab by impact | SentencePiece (T5, ALBERT) |
| **SentencePiece** | Library implementing BPE + Unigram | LLaMA 2, T5, many others |
| **tiktoken** | Fast Rust BPE; `cl100k_base`, `o200k_base` | OpenAI models |

**Key metrics:**
- Vocabulary sizes: 32K (LLaMA 2) → 100K (GPT-4) → 128K (LLaMA 3) → 256K (Gemma)
- Fertility (tokens per word): ~1.3 English; 2–4× for non-English

---

## 2.10 Key Scaling Laws

| Law | Relationship | Reference |
|---|---|---|
| **Kaplan 2020** | L ∝ N^{-0.076} · D^{-0.095} · C^{-0.050} | Original scaling laws |
| **Chinchilla 2022** | Optimal: N_params ≈ D_tokens (20 tokens/param) | Hoffman et al. |
| **Inference scaling (2024)** | Inference compute also scales quality | o1, R1 era |
| **Data quality scaling** | Better data >> more data at same size | FineWeb, DCLM papers |

---

*[← Chapter 1: Models & Providers](./01-foundation-models-and-providers.md) | [Chapter 3: Training Techniques →](./03-training-techniques.md)*
