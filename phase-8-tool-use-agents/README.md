# Phase 8 — Tool Use & AI Agents

> **The action layer.** Everything before this phase was about generating text. This phase
> is about taking actions: calling APIs, writing files, browsing the web, executing code,
> and coordinating multiple AI models to complete complex multi-step tasks.

---

## Why This Phase Matters

The difference between a chatbot and an AI agent is consequentiality. Chatbots generate text.
Agents take actions with real-world effects — and that changes everything:
- A wrong answer in a chatbot is annoying. A wrong action in an agent can delete data, send emails, or transfer money.
- A slow chatbot is frustrating. A looping agent can burn $100 in API costs before you notice.
- A prompt-injected chatbot produces bad text. A prompt-injected agent with tool access can exfiltrate data.

This phase teaches you to build agents that are **capable**, **reliable**, and **safe** — the three
properties that separate production agents from demos.

---

## Sections

| # | Topic | Time Estimate | Status |
|---|---|---|---|
| [8.1](./8.1-function-calling-tool-use.md) | Function Calling & Tool Use: How It Works | 3–4 hours | |
| [8.2](./8.2-designing-good-tools.md) | Designing Good Tools for LLMs | 2–3 hours | |
| [8.3](./8.3-single-agent-patterns.md) | Single-Agent Patterns: ReAct, Plan-and-Execute | 3–4 hours | |
| [8.4](./8.4-multi-agent-systems.md) | Multi-Agent Systems: Orchestrator, Subagents & Handoffs | 4–5 hours | |
| [8.5](./8.5-agent-memory.md) | Agent Memory: Short-Term, Long-Term & Episodic | 3–4 hours | |
| [8.6](./8.6-agent-failure-modes-guardrails.md) | When Agents Go Wrong: Failure Modes & Guardrails | 3–4 hours | |

---

## Prerequisites for This Phase

- [Phase 5 — Building with LLM APIs](../phase-5-building-with-llm-apis/README.md) — tool calling mechanics
- [Phase 7 — RAG](../phase-7-rag/README.md) — agentic RAG as a warm-up
- [4.5 — Prompt Injection & Defense](../phase-4-prompt-engineering/4.5-prompt-injection-and-defense.md)

---

## What You'll Be Able to Do After This Phase

- Build tool-calling agents that interact with external APIs, databases, and systems
- Design tool schemas that LLMs use reliably and correctly
- Implement ReAct and Plan-and-Execute patterns with proper error handling
- Build multi-agent systems where specialized agents collaborate
- Design agent memory systems that persist across sessions
- Identify and defend against the 8 most common agent failure modes

---

## The Stakes Are Higher Here

```
Phase 4 (Prompt Engineering): Wrong output → User gets bad text
Phase 7 (RAG):                Wrong output → User gets wrong answer
Phase 8 (Agents):             Wrong output → Agent takes wrong ACTION
                                             → Real-world consequences
```

The guardrails section (8.6) is not optional reading.

---

## Phase Navigation

| | |
|---|---|
| Previous Phase | [Phase 7 — RAG](../phase-7-rag/README.md) |
| Next Phase | Phase 9 — Evals & Quality *(coming soon)* |
| Back to Roadmap | [Main README](../README.md) |

---

*Last updated: June 2026*
