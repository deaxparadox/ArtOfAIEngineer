# Phase 9 — Evals & Quality

> **The discipline that separates AI engineering from AI experimentation.** You can build a
> working RAG pipeline, a capable agent, or a high-quality prompt in 2 hours. You can't know
> whether it actually works — or whether a change made it better or worse — without evals.

---

## Why This Phase Matters

Every team that ships AI features without evals eventually pays the same tax:
- "We changed the prompt and something broke. But what? We don't know when it was working."
- "Users say quality dropped. We don't know why or since when."
- "We upgraded the model. Is it better? We have no way to tell."

Evals are not a nice-to-have. They're the engineering discipline that makes AI software
maintainable, improvable, and deployable with confidence. In 2026, "Eval Ops" — systematic
measurement infrastructure for AI systems — has become as standard a practice as CI/CD for
traditional software.

---

## Sections

| # | Topic | Time Estimate | Status |
|---|---|---|---|
| [9.1](./9.1-why-evals-are-hard.md) | Why Evals Are the Hardest Part of AI Engineering | 2–3 hours | |
| [9.2](./9.2-types-of-evals.md) | Types of Evals: Unit, Integration, Human, LLM-as-Judge | 3–4 hours | |
| [9.3](./9.3-building-eval-datasets.md) | Building an Eval Dataset That Isn't Garbage | 3–4 hours | |
| [9.4](./9.4-llm-as-judge.md) | LLM-as-Judge: Patterns & Pitfalls | 3–4 hours | |
| [9.5](./9.5-regression-testing.md) | Regression Testing for Non-Deterministic Systems | 3–4 hours | |
| [9.6](./9.6-tracing-and-observability.md) | Tracing & Observability (LangSmith, Langfuse, Helicone) | 3–4 hours | |

---

## Prerequisites for This Phase

- [Phase 7 — RAG](../phase-7-rag/README.md) — specifically 7.5 (RAG Evaluation)
- [Phase 8 — Tool Use & AI Agents](../phase-8-tool-use-agents/README.md) — the systems you're evaluating
- Python testing basics (pytest, assertions)

---

## What You'll Be Able to Do After This Phase

- Design an eval suite that actually predicts production quality
- Choose the right evaluator type for each quality dimension
- Build and curate a golden dataset that stays useful over time
- Use LLM-as-judge reliably, understanding and mitigating its biases
- Wire evals into CI/CD as a deployment gate
- Set up distributed tracing for LLM calls, agents, and RAG pipelines

---

## The Core Shift

```
Before evals:  "I think this prompt is better."
After evals:   "This prompt improved Recall@5 by 8% and faithfulness by 12%
                on the golden dataset. Zero regressions on edge cases."
```

That's the shift this phase teaches.

---

## Phase Navigation

| | |
|---|---|
| Previous Phase | [Phase 8 — Tool Use & AI Agents](../phase-8-tool-use-agents/README.md) |
| Next Phase | Phase 10 — MLOps & Production AI *(coming soon)* |
| Back to Roadmap | [Main README](../README.md) |

---

*Last updated: June 2026*
