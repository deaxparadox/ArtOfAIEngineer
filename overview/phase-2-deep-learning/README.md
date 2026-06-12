# Phase 2 — Deep Learning

> **The architecture layer.** Phase 1 taught you *how* neural networks learn. Phase 2 teaches you *what shapes*
> they take — and why specific shapes were invented to solve specific problems. Every modern LLM is a transformer.
> You cannot meaningfully work with LLMs without understanding what a transformer is and why it replaced
> everything that came before it.

---

## Why This Phase Matters

Understanding deep learning architectures is not about being able to implement them from scratch. It's about
being able to reason about them:

- **Why does GPT work on text but struggle with exact retrieval?** Because it's a transformer, not a database.
- **Why can BERT encode meaning but not generate text?** Because it's encoder-only, not decoder-only.
- **Why does a CNN fail on variable-length text sequences?** Because convolutions assume spatial locality.
- **Why does fine-tuning a pre-trained model take 100× less data than training from scratch?** Because transfer
  learning reuses representations learned from vastly more data.

These are the questions AI engineers face daily. This phase answers them.

---

## Sections

| # | Topic | Time Estimate | Status |
|---|---|---|---|
| [2.1](./2.1-cnns-convolutional-neural-networks.md) | CNNs — Convolutional Layers, Pooling, Image Understanding | 3–4 hours | |
| [2.2](./2.2-rnns-and-lstms.md) | RNNs & LSTMs — Sequential Data, Memory, Vanishing Gradients | 3–4 hours | |
| [2.3](./2.3-attention-mechanism.md) | The Attention Mechanism — The Idea That Changed Everything | 3–4 hours | |
| [2.4](./2.4-transformer-architecture.md) | The Transformer Architecture — Deep Dive | 4–5 hours | |
| [2.5](./2.5-transfer-learning-and-fine-tuning.md) | Transfer Learning & Fine-Tuning Fundamentals | 3–4 hours | |

---

## Prerequisites for This Phase

- All of [Phase 1 — ML Foundations](../phase-1-ml-foundations/README.md)
- Comfortable with PyTorch: tensors, forward pass, training loop
- Understanding of gradient descent, backpropagation, regularization

---

## What You'll Be Able to Do After This Phase

- Read and understand most neural network architecture papers (at the diagram level)
- Explain why transformers replaced RNNs and why that matters
- Build a simple transformer from scratch in PyTorch
- Choose the right architecture class for a given problem type
- Load, adapt, and fine-tune a pre-trained model on a custom task
- Explain multi-head attention, positional encoding, and layer normalization to someone who's never heard of them

---

## The Arc of This Phase

```
2.1 CNNs           → Spatial hierarchy: local patterns → global understanding
2.2 RNNs / LSTMs   → The sequential problem: how to handle variable-length sequences
2.3 Attention      → The insight that made RNNs obsolete
2.4 Transformers   → Attention + everything else = the architecture of LLMs
2.5 Transfer Learning → You don't need to train from scratch. Ever.
```

Each section is a building block for the next. By the end, you'll understand every major architectural
component inside GPT, Claude, BERT, and their successors.

---

## Phase Navigation

| | |
|---|---|
| Previous Phase | [Phase 1 — ML Foundations](../phase-1-ml-foundations/README.md) |
| Next Phase | Phase 3 — Large Language Models *(coming soon)* |
| Back to Roadmap | [Main README](../README.md) |

---

*Last updated: June 2026*
