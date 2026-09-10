# Senior Backend System Design Prep — AI Production Era (2026)

Most system design prep material still teaches the 2023 version of the interview. This repo covers what changed by 2026 — specifically that production AI system design now shows up in general senior backend loops, not just ML-specialist ones — and tries to back the technical claims with primary sources instead of secondhand blog commentary.

## What changed, and why

A few years ago, sketching a load balancer, a database, and a cache, with some scaling talk, could clear a strong loop. That bar moved. Interviewers now grade cost reasoning and operational judgment explicitly rather than treating them as extra credit — "we'd add more servers" reads as a gap, not an answer ([DesignGurus, 2026](https://designgurus.substack.com/p/system-design-interviews-changed)). The harder part to prep for: interviewers have gotten better at probing past a rehearsed answer, and will deliberately shift a requirement partway through specifically to see whether you adapt or just defend the design you walked in with ([source](https://designgurus.substack.com/p/what-changed-in-system-design-interviews)).

The bigger shift is scope. "Design a system that serves an LLM" used to be an ML-track question. By 2026 it's ordinary in general senior backend interviews, next to rate limiters and job schedulers ([Exponent, 2026](https://www.tryexponent.com/blog/system-design-interview-guide); [System Design Handbook](https://www.systemdesignhandbook.com/blog/ai-system-design-interview-questions/)). That's the actual reason this repo exists — most prep material hasn't caught up to that, and the parts that have tend to stop at "here's what RAG is" rather than the production concerns that follow.

A few of the specific, checkable facts behind the AI Production Systems section:

- **Continuous batching is a large, well-documented lever, not folklore.** Iteration-level scheduling — letting a new request join a batch mid-flight instead of waiting for the whole batch to finish — is what the Orca paper introduced, reporting a 36.9x throughput gain over FasterTransformer at matched latency ([Yu et al., OSDI 2022](https://www.usenix.org/system/files/osdi22-yu.pdf)). vLLM's PagedAttention builds on that same idea to fix KV-cache fragmentation, reporting 2-4x further gains over Orca and FasterTransformer ([Kwon et al., SOSP 2023](https://arxiv.org/abs/2309.06180)).
- **Prefill and decode are different workloads, and serving them identically leaves performance on the table.** Prefill is compute-bound; decode is memory-bandwidth-bound. DistServe separates them onto different GPU pools specifically to stop them from interfering with each other ([Zhong et al., 2024](https://arxiv.org/abs/2401.09670)).
- **Guardrails work better as a separate pass than as the same model policing itself.** Anthropic's own agent-building guidance recommends a second model instance to screen inputs/outputs rather than asking one model to both answer and guard itself ([Anthropic Engineering](https://www.anthropic.com/engineering/building-effective-agents)).
- **LLM observability has an actual emerging standard**, not just ad hoc logging — OpenTelemetry's GenAI semantic conventions define shared attributes for token usage, cost, and agent/tool steps, adopted across AWS, GCP, Azure, and Datadog ([OpenTelemetry, 2026](https://opentelemetry.io/blog/2026/genai-observability/)).
- **"Treat evals as infrastructure, not a launch checklist"** is OpenAI's own stated best practice for their evaluation framework — run on every change, not just before shipping ([OpenAI](https://developers.openai.com/api/docs/guides/evaluation-best-practices); [openai/evals](https://github.com/openai/evals)).

None of that is exotic. It's what teams actually running these systems have published about running them, which is a different thing from a listicle summarizing what "AI system design" means.

## What's in here

[`system-design/`](system-design/) — 23 prompts, one file each, in two sections:

- **[AI Production Systems](system-design/README.md#ai-production-systems)** (8 files) — RAG, LLM serving infrastructure, production agent guardrails, AI observability, multi-model routing, evaluation pipelines. Each one walks through the actual mechanism, cites where the claim comes from, and includes a diagram. This is the reason to be here.
- **[Classical Distributed Systems](system-design/README.md#classical-distributed-systems)** (15 files) — the evergreen fundamentals: rate limiters, caches, job schedulers, payments APIs. Worth practicing. Not the differentiator — see [`resources.md`](resources.md) for repos that go deeper on these specifically.

Every prompt ends with a hidden follow-up: design the system, then reveal it and see whether your answer survives the curveball. That's closer to what's actually being graded than the initial design is.

Deliberately not included: a DSA problem set or a behavioral question bank. Both already exist, done well, by other people — linked in [`resources.md`](resources.md) instead of duplicated here.

## How to use it

Start at [`system-design/README.md`](system-design/README.md). Pick one file. Give it the real ~75 minutes — requirements, high-level design, deep dives, cost, failure modes — before you look at the follow-up.

## A note on how this was made

Researched and written with Claude's help, not hand-typed from scratch — the primary-source links above are exactly what I used to check the technical claims before they went in, and I'd rather you verify them than take the repo's word for it. If something in here is wrong or has gone stale, open an issue or a PR.

## License

MIT — use it, fork it, adapt it.
