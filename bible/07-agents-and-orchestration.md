# Chapter 7 — Agents & Orchestration

> Every agent framework, pattern, protocol, and tool in the AI agent ecosystem.

---

## 7.1 Agent Frameworks

### LangChain

The most widely-used LLM application framework. General-purpose; large ecosystem.

| Component | Description |
|---|---|
| **LangChain** | Chains, agents, memory, retrievers |
| **LangGraph** | Stateful agent graphs; production-grade |
| **LangServe** | Deploy chains as REST APIs |
| **LangSmith** | Observability, evals, prompt management |

**LangGraph key concepts:**
- Nodes: functions or LLM calls
- Edges: routing logic (conditional or fixed)
- State: shared dict passed between nodes
- Checkpointing: persist state for recovery
- Human-in-the-loop: pause + resume at any node

**Best for:** Teams heavily invested in LangChain ecosystem; complex stateful workflows.

---

### LlamaIndex

Focused on data ingestion, indexing, and retrieval. Strongest RAG integrations.

| Component | Description |
|---|---|
| **Data connectors** | 100+ sources (Notion, Confluence, S3, etc.) |
| **Indexes** | VectorStore, SummaryIndex, KnowledgeGraph |
| **Query engines** | RAG, sub-question, multi-step |
| **Agents** | ReAct, function calling agents |
| **LlamaCloud** | Managed parsing + indexing |

**Best for:** Document-heavy RAG applications; complex indexing strategies.

---

### CrewAI

Role-based multi-agent coordination. Agents have roles, goals, backstories.

```python
from crewai import Agent, Task, Crew

researcher = Agent(role="Research Analyst", goal="Find key info", ...)
writer     = Agent(role="Content Writer", goal="Write clear report", ...)

crew = Crew(agents=[researcher, writer], tasks=[research_task, write_task])
result = crew.kickoff()
```

**Best for:** Teams with role-based workflows; content creation; research pipelines.

---

### AutoGen (Microsoft)

Multi-agent conversation framework. Agents converse with each other and use tools.

| Pattern | Description |
|---|---|
| **AssistantAgent** | LLM-powered agent |
| **UserProxyAgent** | Human or code-execution proxy |
| **GroupChat** | Multiple agents in conversation |
| **SocietyOfMind** | Nested agent groups |

**Best for:** Research; complex multi-agent systems; code execution pipelines.

---

### OpenAI Agents SDK (2025)

Released March 2025 as production-grade replacement for Swarm.

| Feature | Detail |
|---|---|
| **Agents** | LLM with instructions + tools + handoff capability |
| **Handoffs** | Transfer control + context to specialized agent |
| **Guardrails** | Input/output validation |
| **Tracing** | Built-in observability |
| **OpenAI-native** | Best with GPT models |

**Best for:** OpenAI-native applications needing clean handoff patterns.

---

### Anthropic Agent SDK (2026)

Released alongside Claude 4.6. MCP-integrated.

| Feature | Detail |
|---|---|
| **Tool use** | Native Anthropic tool calling |
| **MCP client** | Connect to any MCP server |
| **Computer use** | Control browser/desktop |
| **Extended thinking** | Configurable reasoning budget |

---

### Semantic Kernel (Microsoft)

Enterprise-focused. Integrates with Azure AI services.

```csharp
// Also available in Python
var kernel = Kernel.CreateBuilder()
    .AddOpenAIChatCompletion("gpt-4o", apiKey)
    .Build();
```

**Best for:** Enterprise; .NET/C# environments; Azure integration.

---

### Haystack (deepset)

Production-grade AI framework with strong eval integration.

| Feature | Detail |
|---|---|
| **Pipelines** | Visual pipeline builder |
| **Components** | Modular; mix any LLM/retriever |
| **Evaluation** | Built-in eval metrics |
| **Self-hosted** | Deploy anywhere |

**Best for:** Production RAG pipelines; strong eval requirements.

---

### DSPy (Stanford, 2023)

Programmatic LLM optimization. Treats prompts as programs that can be compiled and optimized.

```python
class RAG(dspy.Module):
    def __init__(self):
        self.retrieve = dspy.Retrieve(k=3)
        self.respond  = dspy.ChainOfThought("context, question -> answer")
    
    def forward(self, question):
        context = self.retrieve(question)
        return self.respond(context=context, question=question)

# Auto-optimize prompts using labeled examples
teleprompter = dspy.BootstrapFewShot(metric=my_eval_metric)
optimized_rag = teleprompter.compile(RAG(), trainset=train_examples)
```

**Best for:** Teams that want systematic, measurable prompt optimization.

---

## 7.2 The Model Context Protocol (MCP)

**MCP** is an open standard (Anthropic, 2024) for connecting AI models to external tools and data. Now under the Linux Foundation. Adopted by OpenAI, Google, Microsoft, and Anthropic.

```
MCP Architecture:
  Host (Claude, GPT, etc.)
    ↕ MCP Protocol (JSON-RPC over stdio/SSE/HTTP)
  MCP Server (tool provider)
    ↕ Implementation
  External services (GitHub, Slack, databases, etc.)
```

### MCP Primitives

| Primitive | Description | Example |
|---|---|---|
| **Tools** | Functions the model can call | `search_github`, `create_issue` |
| **Resources** | Data the model can read | Files, database records |
| **Prompts** | Reusable prompt templates | System prompts, personas |
| **Sampling** | Model calls initiated from server | Server-side LLM calls |

### MCP Transport

| Transport | Use Case |
|---|---|
| **stdio** | Local tools; subprocess communication |
| **SSE (HTTP)** | Remote servers; streaming |
| **WebSocket** | Bidirectional real-time |

### Notable MCP Servers

| Server | Provides |
|---|---|
| **GitHub MCP** | Repository, issues, PRs, code search |
| **Slack MCP** | Messages, channels, users |
| **Postgres MCP** | Database queries |
| **Filesystem MCP** | File read/write |
| **Brave Search MCP** | Web search |
| **Notion MCP** | Pages, databases |
| **Google Drive MCP** | Files, docs |
| **Puppeteer/Playwright MCP** | Browser automation |

---

## 7.3 Agent Patterns

| Pattern | Description | Framework Support |
|---|---|---|
| **ReAct** | Reason → Act → Observe loop | LangGraph, LlamaIndex, AutoGen |
| **Plan-and-Execute** | Plan all steps; execute separately | LangGraph, custom |
| **Reflexion** | Self-critique and retry on failure | Custom |
| **MCTS-RAG** | Monte Carlo Tree Search for reasoning | Research |
| **Orchestrator-Worker** | Planner delegates to specialists | CrewAI, LangGraph |
| **Handoff** | Transfer full control to specialist | OpenAI Agents SDK |
| **Supervisor** | Quality check on worker outputs | Custom |
| **Swarm** | Decentralized; each agent decides to hand off | OpenAI Swarm (deprecated) |

---

## 7.4 Tool Design Best Practices

| Principle | Rule |
|---|---|
| **Naming** | Verb-first, specific: `search_product_catalog` not `search` |
| **Description** | What it does + when to use + when NOT to use |
| **Parameters** | Every field has a clear description with examples |
| **Output** | Structured JSON the model can reason about |
| **Errors** | Return `{"error": "..."}` not exceptions |
| **Confirmation** | High-risk actions need `confirmed: bool` field |
| **Granularity** | One tool = one atomic operation |
| **Overlap** | No two tools do the same thing |

---

## 7.5 Agent Memory Types

| Memory Type | Storage | Duration | Access Method |
|---|---|---|---|
| **Working memory** | Context window | Session | Direct (in context) |
| **Short-term** | Rolling context buffer | Session | Sliding window |
| **Episodic** | Vector DB + structured DB | Persistent | Semantic retrieval |
| **Semantic (long-term)** | Key-value + vector DB | Persistent | Retrieval |
| **Procedural** | Model weights | Permanent | Learned at training |

---

*[← Chapter 6: RAG & Retrieval](./06-rag-and-retrieval.md) | [Chapter 8: Evaluation & Observability →](./08-evaluation-and-observability.md)*
