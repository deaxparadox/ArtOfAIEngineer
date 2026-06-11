# Phase 4 — Prompt Engineering

> **The craft layer.** You now understand how LLMs work. This phase is about reliably getting
> them to do what you want. Not magic words. Not hacks. Systematic, testable, versioned engineering.

---

## Why This Phase Matters

The gap between "the model can do this" and "the model reliably does this in production" is almost
entirely a prompt engineering problem. A model that scores 92% on a benchmark can produce garbage
on your specific task if the prompt is poorly constructed. Conversely, a well-engineered prompt
on a smaller, cheaper model can match the quality of a poorly-prompted larger one.

In 2026, the discipline has matured past "write clearer instructions." Production prompt engineering
means:
- Versioning prompts like code
- Measuring quality with evals before and after changes
- Treating the prompt as a specification: what must be true about every output?
- Understanding failure taxonomy so you can diagnose regressions systematically

---

## Sections

| # | Topic | Time Estimate | Status |
|---|---|---|---|
| [4.1](./4.1-prompt-anatomy.md) | Prompt Anatomy: System, User & Assistant Turns | 2–3 hours | |
| [4.2](./4.2-few-shot-cot-structured-prompting.md) | Few-Shot, Chain-of-Thought & Structured Prompting | 3–4 hours | |
| [4.3](./4.3-output-formatting-json-tools.md) | Output Formatting: JSON Mode, Tool Calls & Structured Output | 3–4 hours | |
| [4.4](./4.4-failure-modes-and-debugging.md) | Common Failure Modes & How to Diagnose Them | 3–4 hours | |
| [4.5](./4.5-prompt-injection-and-defense.md) | Prompt Injection, Jailbreaks & Defense Strategies | 3–4 hours | |

---

## Prerequisites for This Phase

- All of [Phase 3 — Large Language Models](../phase-3-large-language-models/README.md)
  — especially tokenization, alignment, and hallucinations
- Comfortable calling an LLM API (Anthropic or OpenAI)

---

## What You'll Be Able to Do After This Phase

- Write system prompts that produce consistent, predictable behavior
- Apply few-shot, chain-of-thought, and self-consistency techniques correctly
- Get reliable structured (JSON) output from any major LLM
- Diagnose prompt failures systematically rather than by intuition
- Build prompt injection defenses into production AI applications
- Version, test, and iterate prompts as engineering artifacts

---

## The Shift from "Prompting" to "Context Engineering"

Gartner declared in July 2025: *"Context engineering is in, prompt engineering is out."* The title
changed, the skill didn't. What they meant:

| Old framing (2023) | New framing (2026) |
|---|---|
| Write a good prompt | Design an input context |
| One system prompt | Layered: system + few-shot + retrieved context + tool results |
| Trial and error | Evals-driven iteration |
| Text intuition | Output specification: schema, constraints, success criteria |
| Static prompts | Versioned, tested, deployed like code |

This phase teaches both the craft and the engineering discipline.

---

## Phase Navigation

| | |
|---|---|
| Previous Phase | [Phase 3 — Large Language Models](../phase-3-large-language-models/README.md) |
| Next Phase | Phase 5 — Building with LLM APIs *(coming soon)* |
| Back to Roadmap | [Main README](../README.md) |

---

*Last updated: June 2026*
