# System design prompts

Two sections. **AI Production Systems** is the point of this repo — production AI system design (serving, evaluation, observability, guardrails) reached general senior backend loops in 2026, and most existing prep material is still teaching 2023-era RAG-101. **Classical Distributed Systems** is the evergreen fundamentals — still asked, still worth practicing, but not what makes this repo worth visiting over the alternatives in [`resources.md`](resources.md).

Every prompt has a **"what a strong answer covers"** checklist (the concrete things, not "discuss trade-offs") and a hidden **likely follow-up** — design the system first, then reveal it and see if your design survives the curveball. That adaptation under a shifted requirement is what's actually being graded in 2026, not the initial design.

## Rubric

> Interviewers grade cost and operational reasoning explicitly now — "add more servers" isn't a sufficient answer. They also deliberately shift requirements mid-interview to see if you adapt rather than defend the original design.

- **1** — Don't know how to structure a system design answer.
- **2** — Can list some relevant components but miss requirements-gathering or trade-off discussion.
- **3** — Can produce a reasonable design covering the main components, but weak on cost, failure-mode, or operational discussion.
- **4** — Can drive a structured design (requirements → high-level design → deep dives → trade-offs, including cost and operational burden) at a senior bar.
- **5** — All of the above, plus adapting cleanly when the follow-up shifts the requirements, rather than defending the original design.

---

## AI Production Systems

### Design a RAG-Based Q&A System
*Focus: AI/LLM infrastructure, data modeling · ~75 min*

Design a system that answers questions over a large private document set using retrieval-augmented generation.

**What a strong answer covers:**
- Chunking strategy and why (fixed-size vs. semantic chunking is a real trade-off, not a detail)
- Embedding model choice, and the cost of re-embedding everything when you change it
- Vector store choice and how it actually partitions/scales past a few million vectors
- What happens when retrieval finds nothing relevant — the system should say so, not let the model guess
- Freshness: how new or changed documents get re-indexed without a full rebuild
- How you'd know retrieval quality regressed after a change, before users tell you

<details>
<summary>Likely follow-up (design first, then reveal)</summary>

Users are getting confidently wrong answers when the real answer isn't in the document set at all. How do you detect and fix that class of failure specifically?
</details>

### Design an LLM Serving Gateway
*Focus: AI/LLM infrastructure, scalability · ~75 min*

Design a gateway that sits between your product's backend services and one or more LLM providers/models.

**What a strong answer covers:**
- Continuous (iteration-level) batching vs. static batching — this alone is typically a 4-8x throughput difference, not a minor tuning knob
- Disaggregated prefill/decode: prompt processing and token generation have different resource profiles and often benefit from separate scaling
- VRAM, not raw compute, is usually the actual constraint — model size × bytes-per-parameter (quantization level) + KV cache + runtime overhead
- The quantization trade-off: FP8 roughly halves memory with minimal quality loss; INT4 goes further with more risk
- Multi-provider routing and what happens on a single provider's outage or silent degradation
- GPU utilization sitting below ~60% at peak usually means over-provisioning or bad batching config — not "buy more GPUs"

<details>
<summary>Likely follow-up (design first, then reveal)</summary>

Your primary LLM provider has a regional outage during peak traffic. What's your fallback path, and what does the user actually experience?
</details>

### Design a Customer-Support Chatbot on a Third-Party LLM
*Focus: AI/LLM infrastructure, reliability · ~75 min*

Design a customer-support chatbot on a third-party LLM platform, with access to order history and support docs.

**What a strong answer covers:**
- Safety (hallucination, wrong actions, cost overruns) and security (prompt injection, unauthorized access) are different problems needing different defenses — say both, not just one
- Guardrails belong at the gateway/platform layer, not scattered per-service, for consistent enforcement and a single audit trail
- Explicit tool allowlisting: the bot can only take actions it's been explicitly granted, never implicit ones
- Hard limits (stop completely) vs. soft limits (alert, downgrade to a cheaper model, truncate context) as distinct cost/behavior controls
- Output validation specifically before any irreversible action (a refund, a cancellation) — separate from normal response generation
- A defined escalation path to a human, and what actually triggers it

<details>
<summary>Likely follow-up (design first, then reveal)</summary>

The bot just told a customer it would issue a refund it has no authority to approve. How does your design prevent that from happening again, not just this once?
</details>

### Design a Content Moderation Pipeline Using an LLM
*Focus: AI/LLM infrastructure, cost & operational reasoning · ~75 min*

Design a pipeline that moderates user-generated content (text and images) at scale, mixing cheap classifiers with an LLM for ambiguous cases.

**What a strong answer covers:**
- Tiered approach: cheap classifiers first, LLM only for ambiguous cases — running everything through an LLM is a cost decision dressed up as a quality one
- Latency budget for real-time posting vs. what can go through async/human review instead
- Human review path for edge cases, and how those decisions feed back to improve the cheap tier over time
- What changes in the next hour (tighten the cheap-tier threshold) vs. what changes over the next month (retrain the classifier) when cost spikes

<details>
<summary>Likely follow-up (design first, then reveal)</summary>

Volume just tripled overnight after a viral moment, and your LLM moderation costs tripled with it. What do you change in the next hour, versus what you'd change over the next month?
</details>

### Design an AI Observability & Monitoring Platform
*Focus: AI/LLM infrastructure, observability · ~75 min*

Design a monitoring platform for a company running several LLM-based features in production. Cover what gets measured, how a quality regression gets caught, and how an engineer actually debugs a bad output a real user hit.

**What a strong answer covers:**
- Three distinct layers, each needing different tooling: infrastructure metrics (latency, GPU utilization, error rates), LLM telemetry (token usage, cost per request, full prompt/response pairs), and quality evaluation (accuracy, hallucination rate, user feedback signals)
- Full traceability as foundational, not optional: if you can't reconstruct exactly what a request or agent did, you can't debug it in production
- Drift detection on both sides: input distribution changes (what users are actually asking) and output distribution changes (how the model responds), which matters even more when the model is a third-party API you don't control
- What "rollback" actually means for a prompt or model change, and how fast you can execute it

<details>
<summary>Likely follow-up (design first, then reveal)</summary>

A single bad prompt-template change caused a silent quality regression that took two weeks to notice. What's missing from your design that would have caught it in two hours instead?
</details>

### Design a Multi-Model Routing & Fallback System
*Focus: AI/LLM infrastructure, cost & operational reasoning · ~75 min*

Design a system that routes each request to the right model across multiple providers/tiers based on task difficulty, and fails over gracefully when a provider degrades or goes down.

**What a strong answer covers:**
- The router itself has to be cheap — using your most expensive model to decide which model to use defeats the entire point
- Classify-then-route (decide up front) vs. cascade-and-escalate (try cheap first, escalate on failure) are different strategies with different latency/cost shapes
- Fallback behavior on an outage — a different provider, a cached/cheaper response, or a visible failure — and that the right choice depends on the specific feature
- The same prompt can behave meaningfully differently across models, so routing isn't "free" even when it's nominally the same task

<details>
<summary>Likely follow-up (design first, then reveal)</summary>

Your primary provider's latency triples during their own incident, but it never actually errors out. Your health checks don't catch it. What's actually broken in your design?
</details>

### Design a Production AI Agent Platform with Guardrails
*Focus: AI/LLM infrastructure, reliability, cost & operational reasoning · ~75 min*

Design the platform underneath an autonomous AI agent that takes real actions in production, not just answers questions. Cover specifically how you'd prevent it from running away — in cost or in real-world actions.

**What a strong answer covers:**
- Termination logic is deceptively hard: agents that don't know when to stop cause more production incidents than agents that fail outright
- Budget limits and fallback paths at every level of the call stack, not just the top
- Output validation specifically before any irreversible action, as a distinct step from normal generation
- A documented eval suite covering happy path, edge cases, and adversarial inputs — built before the first real user, not written after an incident
- A staged rollout plan and a defined human escalation path

<details>
<summary>Likely follow-up (design first, then reveal)</summary>

The agent has been looping for 40 minutes on a task that should take 2, burning budget the whole time, and nobody noticed until the bill arrived. Where exactly did your design fail to catch this?
</details>

### Design an LLM Evaluation Pipeline
*Focus: AI/LLM infrastructure, observability · ~75 min*

Design the evaluation pipeline a team runs before shipping any change to a prompt, model, or fine-tune, so a regression gets caught before it reaches users.

**What a strong answer covers:**
- A golden/regression test set every change runs against before shipping — not ad hoc spot checks by whoever made the change
- Offline evaluation (against the golden set) and online evaluation (real traffic, user feedback signals) catch different failure classes and you need both
- Who or what actually judges quality — human review, a separate "judge" model, or hard-coded checks — and the real trade-offs of each
- How you evaluate something fuzzy like "technically correct but unhelpful," not just factual correctness

<details>
<summary>Likely follow-up (design first, then reveal)</summary>

A prompt change passed every golden-set test but caused a real quality drop for a class of query nobody had written a test for. How would you have caught that class of failure?
</details>

---

## Classical Distributed Systems

### Design a URL Shortener
*Focus: Scalability, data modeling · ~75 min*

Design a service like bit.ly: given a long URL, generate a short one that redirects to it.

**What a strong answer covers:**
- ID generation approach (counter + base62 vs. hash) and how you'd handle collisions
- The read/write ratio (reads vastly outnumber writes) and what that implies for caching
- Adding custom slugs and per-link analytics without slowing down the redirect path
- What the redirect service does when its backing store is briefly unavailable

<details>
<summary>Likely follow-up (design first, then reveal)</summary>

Now a marketing team wants custom, human-readable slugs and click analytics per link, without slowing down redirects. How does your design change?
</details>

### Design a Rate Limiter
*Focus: API design, scalability · ~75 min*

Design a rate limiter for a public API.

**What a strong answer covers:**
- Algorithm trade-off: token bucket allows bursts, sliding window is smoother, fixed window is simplest but bursty at window boundaries
- Where enforcement actually lives (gateway vs. per-service) and why that matters for correctness once you're distributed
- Per-user vs. per-IP vs. per-API-key limits, and what each is actually protecting against
- What happens when the limiter's own datastore is unavailable — fail open or fail closed, and why

<details>
<summary>Likely follow-up (design first, then reveal)</summary>

One customer is on a burst-heavy usage pattern that keeps tripping the limiter and generating support tickets. What would you change, and what does it cost you?
</details>

### Design a Distributed Cache
*Focus: Caching, consistency trade-offs · ~75 min*

Design a distributed in-memory cache used by many services.

**What a strong answer covers:**
- Eviction policy choice (LRU/LFU/TTL) matched to the actual access pattern
- Partitioning strategy (consistent hashing) and what happens to the cluster on node failure or rebalance
- Cache invalidation strategy and the staleness window it implicitly creates
- Thundering-herd protection when a single hot key expires under heavy concurrent load

<details>
<summary>Likely follow-up (design first, then reveal)</summary>

A node in the cache cluster just died. Walk through exactly what happens in the next 30 seconds, and what your users experience.
</details>

### Design a Notification System
*Focus: Scalability, reliability · ~75 min*

Design a system that sends notifications (email, SMS, push) triggered by events across a product.

**What a strong answer covers:**
- Why a queue sits between the trigger and delivery, and the fan-out architecture that follows from it
- Per-channel retry/backoff and dead-lettering for permanent failures
- Per-user rate limiting so one noisy feature can't spam a user across every channel at once
- How you'd detect a silent delivery failure — a provider that accepts the message but never actually delivers it

<details>
<summary>Likely follow-up (design first, then reveal)</summary>

The SMS provider starts silently dropping 5% of messages with no error response. How would you even detect that, and what's your mitigation?
</details>

### Design a News Feed
*Focus: Data modeling, scalability · ~75 min*

Design a social news feed.

**What a strong answer covers:**
- Fan-out-on-write vs. fan-out-on-read, and the celebrity-account problem that breaks pure fan-out-on-write
- Feed storage model and how ranking gets computed without recomputing from scratch on every request
- How much staleness the feed can tolerate vs. where you actually need strict consistency

<details>
<summary>Likely follow-up (design first, then reveal)</summary>

One account has 50 million followers and posts several times a day. Does your fan-out strategy still hold, and if not, what breaks first?
</details>

### Design a Distributed Job Scheduler
*Focus: Reliability, consistency trade-offs · ~75 min*

Design a system that schedules and reliably executes jobs (cron-like and one-off) across a fleet of workers.

**What a strong answer covers:**
- At-least-once vs. exactly-once execution, and why exactly-once is expensive and often unnecessary
- Leader election or locking to stop two workers from claiming the same job
- Handling a worker crash mid-job — idempotent retries or checkpointing, not just "retry from scratch"
- Clock skew's effect on cron-style scheduling across a fleet of machines

<details>
<summary>Likely follow-up (design first, then reveal)</summary>

Two workers just picked up the same job at the same time because of a scheduling race. How does your design prevent or recover from that?
</details>

### Design a Chat/Messaging System
*Focus: Consistency trade-offs, scalability · ~75 min*

Design a 1:1 and group messaging system.

**What a strong answer covers:**
- Message ordering is per-conversation, not global — and that's a meaningfully cheaper guarantee to provide
- Delivery guarantee (usually at-least-once with client-side dedup, not exactly-once)
- How read receipts avoid becoming their own scaling problem in large groups
- Delivering messages correctly to a user who reconnects after being offline

<details>
<summary>Likely follow-up (design first, then reveal)</summary>

A group chat has 500 members and someone sends a message every second. What's your bottleneck, and how do you keep read receipts from making it worse?
</details>

### Design an Idempotent Payments API
*Focus: API design, reliability, cost & operational reasoning · ~75 min*

Design the API and backend for processing payments where retries are expected (client timeouts, network failures).

**What a strong answer covers:**
- Idempotency key design, and that it must be checked before any side effect occurs, not after
- An explicit state machine for a payment's lifecycle, so a retry can't skip or repeat a state
- A reconciliation process for when your state machine and the payment provider's records disagree
- Separating the API's fast synchronous response from the actual asynchronous settlement

<details>
<summary>Likely follow-up (design first, then reveal)</summary>

Finance reports a small number of double-charges last month despite idempotency keys. Where would you actually look, and how would you prevent recurrence?
</details>

### Design Search Autocomplete
*Focus: Caching, scalability · ~75 min*

Design a typeahead/autocomplete system for a search box.

**What a strong answer covers:**
- Data structure trade-off: a trie for prefix matching vs. precomputed top-k suggestion lists
- Freshness requirement — how new or trending terms get in without a full rebuild
- The latency budget (usually sub-100ms) and what that rules out architecturally
- Global suggestions vs. personalized ones, and what personalization actually costs

<details>
<summary>Likely follow-up (design first, then reveal)</summary>

Trending searches need to show up in suggestions within minutes, not the next daily batch job. What has to change?
</details>

### Design a Log/Metrics Aggregation Pipeline
*Focus: Observability, scalability, cost & operational reasoning · ~75 min*

Design a pipeline that ingests logs/metrics from thousands of services and makes them queryable.

**What a strong answer covers:**
- Ingestion architecture that absorbs a volume spike without falling over (buffering, backpressure)
- Hot vs. cold storage trade-off and what it means for query latency on older data
- A sampling strategy and being explicit about what you're willing to lose to control cost
- Keeping the pipeline usable during the exact incident that's generating the volume spike

<details>
<summary>Likely follow-up (design first, then reveal)</summary>

Storage costs for this pipeline just became the single largest infra line item. What do you cut, and how do you decide what's safe to lose?
</details>

### Design a Multi-Tenant SaaS Backend
*Focus: Data modeling, reliability · ~75 min*

Design the data layer for a B2B SaaS product serving many customers (tenants).

**What a strong answer covers:**
- Isolation strategy (shared schema with a tenant_id vs. schema-per-tenant vs. database-per-tenant) and the operational cost of each
- Noisy-neighbor protection so one tenant's load can't degrade everyone else's
- Supporting one tenant's schema customization without forking the entire data model
- Tenant-level backup, restore, and data deletion for compliance

<details>
<summary>Likely follow-up (design first, then reveal)</summary>

Your single largest customer just asked for a contractual guarantee that their data never shares infrastructure with anyone else. What does that actually cost you to support?
</details>

### Design a File Storage/Sharing Service
*Focus: Data modeling, scalability · ~75 min*

Design a service like Dropbox: upload, store, sync, and share files.

**What a strong answer covers:**
- Chunking strategy for large files and how resumable uploads work
- Deduplication via content-addressed storage, and its privacy implications
- Sync conflict resolution when two clients edit the same file offline
- Access control model for sharing — link-based vs. ACL-based, and when each is appropriate

<details>
<summary>Likely follow-up (design first, then reveal)</summary>

Two people edit the same file offline on different laptops and reconnect at the same time. Walk through exactly what each of them sees.
</details>

### Design a Leaderboard/Ranking System
*Focus: Data modeling, consistency trade-offs · ~75 min*

Design a real-time leaderboard for a game or platform with millions of users.

**What a strong answer covers:**
- A data structure for fast rank lookups at scale (sorted sets / skip lists), not a naive sort on every read
- Consistent, defined tie-handling
- Whether every score update needs to be reflected instantly, or a small lag is acceptable
- Scoped views (like "rank among my friends") without maintaining a full separate leaderboard per scope

<details>
<summary>Likely follow-up (design first, then reveal)</summary>

Someone asks for "my rank among just my friends," computed live, not the global leaderboard. Does your data structure still work?
</details>

### Design a Distributed Unique ID Generator
*Focus: Consistency trade-offs, scalability · ~75 min*

Design a service that generates globally unique, roughly time-sortable IDs across many machines without a central bottleneck.

**What a strong answer covers:**
- Why a central auto-increment doesn't scale, and what replaces it (Snowflake-style: timestamp + machine ID + sequence)
- Clock skew's effect on time-sortability specifically
- Collision avoidance across machines without requiring coordination on every ID
- What happens at ID exhaustion or sequence rollover under high throughput

<details>
<summary>Likely follow-up (design first, then reveal)</summary>

One data center's clock drifts 200ms behind the others for an hour. What actually breaks, and how would you even notice?
</details>

### Design an On-Call Alerting System
*Focus: Reliability, observability · ~75 min*

Design a system like PagerDuty: route alerts from monitoring systems to the right on-call engineer, with escalation if unacknowledged.

**What a strong answer covers:**
- Escalation policy design and what happens when nobody acknowledges an alert
- Deduping/grouping correlated noisy alerts so one root cause doesn't page five people separately
- The alerting path's own reliability — it can't depend on the systems it exists to alert about
- Correct on-call scheduling and handoff across time zones

<details>
<summary>Likely follow-up (design first, then reveal)</summary>

The alerting system itself is down during an incident — the thing meant to page people about outages is having one. How did you design around that, if at all?
</details>
