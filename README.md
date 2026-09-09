# Senior Backend System Design Prep — AI Production Era (2026)

Most system design prep material still teaches the 2023 version of the interview. This repo is narrowly focused on what actually changed by 2026, backed by sources, not vibes.

## What changed

**The bar moved from "does it scale" to "does it survive production."** A few years ago, sketching a load balancer, a database, and a cache with some scaling talk could pass a strong loop. That's no longer sufficient — interviewers now grade cost reasoning and operational judgment explicitly, not as a bonus. "We'd just add more servers" reads as a red flag, not an answer. ([source](https://designgurus.substack.com/p/system-design-interviews-changed))

**AI/LLM infrastructure design is now mainstream for backend roles, not ML-specialist-only.** A year or two ago, "design a system that serves an LLM" was reserved for ML engineering loops. By 2026 it's a standard category in general senior backend interviews, alongside classic distributed systems, real-time systems, and data pipelines. You're expected to reason about chunking, embeddings, vector stores, retrieval, and LLM-serving trade-offs the way you'd reason about a cache or a queue — as a normal part of the toolkit, not a specialty. ([source](https://www.tryexponent.com/blog/system-design-interview-guide), [source](https://www.systemdesignhandbook.com/blog/ai-system-design-interview-questions/))

**Production AI systems have their own hard-won lessons, and they're now fair game:**
- Continuous (iteration-level) batching over static batching is typically a 4-8x throughput difference in LLM serving — a genuinely large, non-obvious lever. ([source](https://tianpan.co/blog/2026-04-09-continuous-batching-llm-inference))
- VRAM, not raw compute, is usually the actual bottleneck in serving — driven by model size, quantization level, and KV cache overhead, not FLOPs. ([source](https://www.sitepoint.com/the-2026-definitive-guide-to-running-local-llms-in-production/))
- Observability is the piece most candidates skip, and it's treated as foundational now: if you can't trace and roll back an agent's behavior, it doesn't pass. A real production stack has three distinct layers — infra metrics, LLM telemetry, and quality evaluation. ([source](https://valuestreamai.com/blog/ai-monitoring-in-production-guide-2026))
- Agents that don't know when to **stop** cause more production incidents than agents that fail outright — termination logic is a real, deceptively hard design problem, not an afterthought. ([source](https://medium.com/@dewasheesh.rana/agentic-ai-in-production-designing-autonomous-multi-agent-systems-with-guardrails-2026-guide-a5a1c8461772))
- Guardrails belong at the gateway/platform layer for consistent enforcement, not scattered per-service — and cost controls (hard limits that stop an agent vs. soft limits that just downgrade it) are the first guardrail to design in, not the last one bolted on. ([source](https://www.getmaxim.ai/articles/the-complete-ai-guardrails-implementation-guide-for-2026/))

**Interviewers deliberately shift requirements mid-interview.** When every candidate walks in with the same memorized architecture, interviewers stop getting signal from the initial design — so they probe with follow-ups that change the constraints partway through, specifically to see whether you adapt or defend. ([source](https://designgurus.substack.com/p/what-changed-in-system-design-interviews))

## What's in here

[`system-design.md`](system-design.md) is the actual content — 19 prompts split into two sections:

- **AI Production Systems** (8 prompts) — RAG, LLM serving infrastructure, production agent guardrails, AI observability, multi-model routing, evaluation pipelines. This is the part that doesn't already exist elsewhere in this form.
- **Classical Distributed Systems** (11 prompts) — the evergreen fundamentals (rate limiters, caches, job schedulers, payments APIs). Still worth practicing, not what makes this repo different from the alternatives below.

Every prompt has a **"what a strong answer covers"** checklist — concrete things, not "discuss trade-offs" — and a hidden **likely follow-up** curveball. Design the system first, then reveal it and see if your design survives.

This repo intentionally does **not** include a DSA problem set or a behavioral question bank — those already exist, done well, elsewhere. See [`resources.md`](resources.md).

## How to use it

Pick one prompt. Give it the full ~75 minutes: requirements, high-level design, deep dives, trade-offs, cost. Then reveal the follow-up and think through how your design actually holds up. That adaptation is the skill being graded in 2026 — not the initial design.

## License

MIT — use it, fork it, adapt it. Corrections and additions welcome via PR.
