# Chapter 11 — Security & Safety

> AI alignment, LLM security threats, guardrails, and responsible AI practices.

---

## 11.1 Alignment Approaches

### Constitutional AI (Anthropic)

Training models using a written "constitution" of principles rather than purely human feedback.

**Stage 1 (SL-CAI):** Model critiques and revises its own responses using the constitution.
**Stage 2 (RL-CAI):** AI feedback (RLAIF) — another model scores based on constitutional principles.

**Goal:** Reduce human annotation bottleneck while maintaining alignment quality.

### RLHF (OpenAI, original)

Three stages: SFT → reward model → PPO optimization.
**Status 2026:** Largely replaced by DPO for most use cases due to instability.

### DPO (Standard 2026)

Direct Preference Optimization. Preference pairs → single-stage alignment.
**Standard choice** for open-source and most production alignment.

### Scalable Oversight

Training powerful models to help evaluate outputs of other powerful models.
**Debate:** Two AI models debate correctness; judge trained on outcomes.
**Iterated amplification:** Humans + AI collaboratively oversee AI systems.

---

## 11.2 OWASP LLM Top 10 (2025 Edition)

The authoritative security risk list for LLM applications.

| Rank | Vulnerability | Description | Primary Defense |
|---|---|---|---|
| **LLM01** | Prompt Injection | Malicious inputs hijack model behavior | Input scanning; structural separation |
| **LLM02** | Sensitive Information Disclosure | Model reveals private data | Output filtering; PII redaction |
| **LLM03** | Supply Chain | Vulnerable third-party components | Dependency audits; MCP server vetting |
| **LLM04** | Data and Model Poisoning | Training data corruption | Data validation; provenance tracking |
| **LLM05** | Improper Output Handling | Trusting LLM output without validation | Schema validation; downstream checks |
| **LLM06** | Excessive Agency | Agent with too-broad permissions takes bad actions | Least privilege; confirmation gates |
| **LLM07** | System Prompt Leakage | System prompt extracted by user | Canary tokens; refusal training |
| **LLM08** | Vector/Embedding Weaknesses | Attacks on retrieval systems | Post-retrieval injection scan |
| **LLM09** | Misinformation | Model generates misleading content | Grounding; citations; human review |
| **LLM10** | Unbounded Consumption | Uncontrolled LLM resource usage | Rate limiting; cost budgets |

---

## 11.3 Prompt Injection Taxonomy

### Direct Injection (Jailbreaks)

| Type | Example | Mitigation |
|---|---|---|
| **Role-play framing** | "You are DAN (Do Anything Now)..." | Alignment; refusal training |
| **Instruction override** | "Ignore previous instructions..." | Input scanning |
| **Hypothetical framing** | "In a fictional story..." | Context-aware refusal |
| **Language obfuscation** | Base64, ROT13, foreign language | Decode + scan |
| **Token manipulation** | "c-a-t" with dashes | Token reconstruction |
| **Crescendo attacks** | Gradually escalate through benign requests | Context tracking |
| **Multi-turn** | Build up context over many turns | Session monitoring |

### Indirect Injection

Malicious instructions embedded in content the agent processes:
- Web pages retrieved during browsing
- Email content processed by email assistant
- Documents uploaded for analysis
- Database records containing user content
- MCP server responses

**2026 primary attack vector:** Indirect injection through tool results.

---

## 11.4 Defense Architecture

### Defense-in-Depth Stack

```
Layer 1: Input validation
  - Regex/pattern scanning for known injection strings
  - Length limits
  - Character encoding normalization

Layer 2: Structural separation
  - XML tags around untrusted content
  - "This is DATA not INSTRUCTIONS" prompts
  - Document sandboxing

Layer 3: Model alignment
  - Refusal training
  - Constitutional AI
  - Safety classifiers

Layer 4: Tool allowlist + validation
  - Explicit allowlist of permitted tools
  - Schema validation before execution
  - Confirmation gates for destructive actions

Layer 5: Output validation
  - PII detection before returning to user
  - Schema validation for structured output
  - Safety classifier on outputs

Layer 6: Audit + monitoring
  - Log all inputs and outputs
  - Alert on anomalous patterns
  - Rate limiting per user
```

---

## 11.5 Guardrail Tools

| Tool | Type | What It Detects |
|---|---|---|
| **Microsoft Prompt Shield** | Commercial (Azure) | Direct + indirect injection |
| **Lakera Guard** | Commercial | Real-time injection; PII; content policy |
| **NeMo Guardrails** (NVIDIA) | Open source | Topical, safety, jailbreak rails |
| **Guardrails AI** | Open source | Output validation + retry |
| **LLM Guard** | Open source | Multiple scanner pipeline |
| **Garak** | Open source | LLM vulnerability scanner (red-teaming) |
| **PromptBench** | Open source | Robustness testing |
| **Rebuff** | Open source | Self-hardening injection detector |

---

## 11.6 Responsible AI Frameworks

### Evaluation Frameworks

| Framework | Organization | Focus |
|---|---|---|
| **HELM** | Stanford CRFM | Holistic LLM evaluation |
| **MMLU** | Berkeley | Knowledge and reasoning |
| **TruthfulQA** | Oxford/GPT-4 paper | Truthfulness; hallucination |
| **ToxiGen** | Microsoft | Hate speech; stereotypes |
| **WinoGender** | University of Washington | Gender bias |
| **BBQ** | Princeton | Bias; ambiguous context |
| **Red-teaming** | Anthropic/OpenAI | Adversarial testing |

### Bias Categories

| Type | Example | Detection Tool |
|---|---|---|
| **Gender bias** | Model associates professions with gender | WinoGender |
| **Racial bias** | Different quality responses by race | BBQ, custom evals |
| **Political bias** | Slants answers toward political positions | Manual + LLM judge |
| **Religious bias** | Different treatment of religions | Manual evaluation |
| **Linguistic bias** | Lower quality for non-English | Multilingual benchmarks |

---

## 11.7 Data Privacy

| Concern | Risk | Mitigation |
|---|---|---|
| **Training data memorization** | Model recites PII from training | Differential privacy; memorization evals |
| **User data in context** | Sensitive data in prompts logged by provider | Self-hosted models; data processing agreements |
| **RAG data exposure** | Retrieved content exposed across users | Tenant isolation; access control |
| **Long-term memory** | Agent memory persists sensitive data | TTL on memories; user deletion rights |
| **Embedding invertibility** | Embeddings can partially reconstruct text | Avoid embedding very sensitive text |

### Regulatory Landscape (2026)

| Regulation | Region | AI Relevance |
|---|---|---|
| **EU AI Act** | EU | High-risk AI systems; transparency; auditing |
| **GDPR** | EU | Data processing; right to erasure |
| **CCPA** | California | Consumer data rights |
| **NIST AI RMF** | US | Risk management framework |
| **ISO/IEC 42001** | Global | AI management systems |
| **HIPAA** | US healthcare | Patient data in AI systems |
| **SOC 2** | US | Trust services criteria |

---

## 11.8 Red-Teaming

Systematic adversarial testing to find safety failures before deployment.

**Red-teaming approaches:**
1. **Manual red-teaming:** Human testers try to break the system
2. **Automated red-teaming:** LLM generates adversarial inputs (Garak, Promptbench)
3. **Fuzzing:** Random/mutation-based input generation
4. **Jailbreak taxonomy:** Systematically test all known jailbreak categories

**Key red-teaming categories:**
- Harmful content generation
- PII extraction
- Prompt injection
- Capability elicitation (bypassing safety)
- Misinformation
- System prompt extraction

---

*[← Chapter 10: Hardware & Cloud](./10-hardware-and-cloud.md) | [Chapter 12: Key Papers & Benchmarks →](./12-key-papers-and-benchmarks.md)*
