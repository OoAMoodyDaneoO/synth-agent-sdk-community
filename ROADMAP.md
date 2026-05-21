# Synth Roadmap

This document outlines what we're working on and what's coming next. It's a living document — priorities shift based on community feedback and real-world usage.

Want to influence the roadmap? Open a [Roadmap Feedback discussion](../../discussions/new?category=roadmap-feedback) or +1 an existing feature request.

---

## Current: v2.2.x (shipped)

- ✅ Multi-agent topology picker at `synth init` (pipeline, graph, team, debate, critic-review, consensus)
- ✅ A2A external interoperability (`A2AClientTool`, `A2AServerAdapter`) with SSRF protection
- ✅ Synth Dev Space cloud deployment (CloudFront + Fargate + Cognito, single `synth deploy --target cloud`)
- ✅ AgentCore observability native (X-Ray traces, CloudWatch metrics, runtime telemetry in Dev Space UI)
- ✅ AgentCore memory and evaluations (conversation history from AgentCore Memory, Evaluations tab)
- ✅ Unified pricing feed — real-time cost tracking within 1% of provider invoices
- ✅ `RalphLoop` — autonomous run-test-fix iteration with checkpointing and streaming
- ✅ `Guard.no_pii_output(action=GuardAction.redact)` — redact mode in addition to block
- ✅ AgentCore registry publishing (`synth agents publish`)
- ✅ DynamoDB memory backend (`Memory.dynamodb(...)`)

---

## In progress: v2.3.0

These are actively being designed or implemented.

### Per-tool guards
Attach guard policies directly to individual tools rather than at the agent level. Express "allow `web_search` freely, require approval before `shell`" without splitting into separate agents.

```python
@tool(guards=[Guard.require_approval()])
def execute_shell(command: str) -> str:
    ...
```

### Long-term cross-session memory
Semantic memory that retrieves relevant context *across* thread IDs — not just within a single conversation. Remembering what a user said two weeks ago in a different session. Builds on the existing `SemanticMemory` + `BaseVectorStore` foundation.

### `ToolSelector` — dynamic tool relevance scoring
Automatically narrow the active tool set per invocation based on task context. Prevents performance degradation when an agent has 20+ tools registered. Configurable scoring strategies (embedding similarity, keyword match, LLM-based).

### Circuit breaker for graph execution
Live fault isolation during parallel graph execution. When a branch enters a failure loop or hits sustained rate limits, isolate it and route around it without aborting the whole graph run.

### Native agent-loop multimodal
First-class support for interleaved multimodal inputs in the agent's core reasoning loop — not just as tool parameter types. Send a screenshot mid-conversation and have the agent reason over it natively.

---

## Planned: v2.4.0

Designed but not yet in active development. Subject to change based on community feedback.

### Self-reflective critique loop
A structured self-correction primitive where the agent evaluates its own output against a configurable rubric and revises before returning — distinct from `RalphLoop`'s external predicate model. Think of it as `RalphLoop` where the predicate is an LLM judge.

### Cross-agent shared memory bus
A `SharedMemory` or `TeamContext` primitive that lets agents in a team read each other's working state directly, without routing everything through the orchestrator. Useful for research team topologies where agents need to build on each other's notes.

### Richer routing policy language
Extend the `HybridRouter` / `RuleRouter` with additional routing dimensions: agent availability/load, agent historical track record on similar task types, and cost-target-based routing. Currently routes on task keywords, message length, agent roles, and LLM judgment.

### Per-agent cost budgets in multi-agent runs
Set cost ceilings per agent within a single team execution so one runaway agent can't consume the entire run budget. Builds on the existing `CostAttribution` infrastructure.

---

## Under consideration / community-requested

These are ideas we've heard but haven't committed to. Vote with 👍 on the linked discussions or open a new one.

- Adaptive retry strategies that change approach on failure (decompose task, escalate to human) rather than just repeating the same call
- `ToolSelector` with LLM-based relevance scoring (v2.3 ships embedding/keyword; LLM scoring is a follow-on)
- First-party vector store integrations (Pinecone, Weaviate, pgvector) for `SemanticMemory`
- Agent versioning UI in Dev Space (currently CLI-only via `Version` / `CanaryRouter`)
- Streaming through A2A handoffs

---

## How we prioritise

1. **Correctness and reliability** — bugs in shipped features before new features
2. **Production blockers** — things that prevent real deployments from working
3. **Community signal** — features with the most +1s and concrete use cases
4. **Strategic fit** — features that make the full lifecycle (build → deploy → govern → observe) more coherent

If something you need isn't on this list, open a [feature request](../../issues/new?template=feature_request.md).
