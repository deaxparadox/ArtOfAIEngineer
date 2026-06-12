# Phase 5 — Building with LLM APIs

> **The engineering layer.** Phases 3 and 4 taught you to understand models and write prompts.
> This phase is about shipping production software that calls LLM APIs reliably, efficiently,
> and cheaply. The gap between "works in playground" and "works in production at scale" is 
> almost entirely what this phase covers.

---

## Why This Phase Matters

Every AI engineer eventually hits a wall where:
- The API returns a 429 and the request dies silently
- Streaming cuts off mid-sentence for 2% of users
- The monthly bill is 10× what was budgeted
- The latency is fine at 10 users but collapses at 1,000
- A model update silently changes behavior

None of these are prompt problems. They're infrastructure problems. This phase solves them.

---

## Sections

| # | Topic | Time Estimate | Status |
|---|---|---|---|
| [5.1](./5.1-provider-apis.md) | Working with AI Provider APIs (Anthropic, OpenAI, Gemini) | 3–4 hours | |
| [5.2](./5.2-streaming-and-async.md) | Streaming Responses & Async Patterns | 3–4 hours | |
| [5.3](./5.3-token-counting-and-cost.md) | Token Counting, Cost Estimation & Budget Management | 3–4 hours | |
| [5.4](./5.4-prompt-caching.md) | Prompt Caching: What It Is & When to Use It | 2–3 hours | |
| [5.5](./5.5-errors-retries-rate-limits.md) | Handling Errors, Retries, Rate Limits & Fallbacks | 3–4 hours | |
| [5.6](./5.6-multimodal.md) | Multi-Modal: Images, Audio & Documents | 3–4 hours | |

---

## Prerequisites for This Phase

- All of [Phase 3 — Large Language Models](../phase-3-large-language-models/README.md)
- All of [Phase 4 — Prompt Engineering](../phase-4-prompt-engineering/README.md)
- Python async/await basics
- Basic HTTP knowledge (status codes, headers, request/response)

---

## What You'll Be Able to Do After This Phase

- Call Anthropic, OpenAI, and Gemini APIs with production-grade code
- Implement streaming with proper error handling and graceful degradation
- Track token usage per user/feature and enforce cost budgets
- Cut API costs 50–90% with prompt caching for repeated system prompts
- Build resilient retry logic with jitter, circuit breakers, and provider fallbacks
- Send images, PDFs, and audio to multimodal models

---

## The Production Maturity Ladder

```
Level 1 (Prototype): Single API call, no error handling, no monitoring
Level 2 (Beta):      Basic retries, hardcoded system prompt, rough cost awareness
Level 3 (Production): Full retry logic + jitter, prompt caching, cost tracking per user,
                       rate-limit awareness, streaming, structured output, fallback providers
Level 4 (Scale):     Circuit breakers, multi-provider routing, batch APIs for async workloads,
                     KV-cache optimization, observability pipeline
```

Most teams ship at Level 2 and wonder why their AI features are flaky and expensive.
This phase takes you to Level 3–4.

---

## Phase Navigation

| | |
|---|---|
| Previous Phase | [Phase 4 — Prompt Engineering](../phase-4-prompt-engineering/README.md) |
| Next Phase | Phase 6 — Embeddings & Semantic Search *(coming soon)* |
| Back to Roadmap | [Main README](../README.md) |

---

*Last updated: June 2026*
