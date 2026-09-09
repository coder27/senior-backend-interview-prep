# System design prompts

19 prompts for senior-level system design practice, refreshed for 2026: cost and operational reasoning are graded explicitly now (not just "add more servers"), AI/LLM infrastructure questions now reach general senior backend loops (not just ML roles), and interviewers deliberately shift requirements mid-interview to see if you adapt rather than recite a memorized architecture.

Each prompt has a **likely follow-up** — a curveball an interviewer would plausibly raise partway through. Design the system first, then reveal it and think through how your design holds up. That's the actual practice, not the initial design.


## Rubric

> As of 2026, interviewers grade cost and operational reasoning explicitly (not just 'add more servers'), and deliberately shift requirements mid-interview to see if you adapt rather than recite a memorized architecture. The 'likely follow-up' on each prompt is there to practice exactly that.

- **1** — Don't know how to structure a system design answer.
- **2** — Can list some relevant components but miss requirements-gathering or trade-off discussion.
- **3** — Can produce a reasonable design covering the main components, but weak on cost, failure-mode, or operational discussion.
- **4** — Can drive a structured design (requirements -> high-level design -> deep dives -> trade-offs, including cost and operational burden) at a senior bar.
- **5** — All of the above, plus adapting cleanly when the follow-up shifts the requirements, rather than defending the original design.

## Prompts


### Design a URL Shortener
*Focus: Scalability, Data Modeling · ~75 min*

Design a service like bit.ly: given a long URL, generate a short one that redirects to it. Cover ID generation, read/write ratio, and how you'd scale reads.

<details>
<summary>Likely follow-up (design first, then reveal)</summary>


Now a marketing team wants custom, human-readable slugs and click analytics per link, without slowing down redirects. How does your design change?

</details>

### Design a Rate Limiter
*Focus: API Design, Scalability · ~75 min*

Design a rate limiter for a public API. Cover algorithm choice (token bucket, sliding window, etc.), where it lives (client, gateway, service), and behavior in a distributed deployment.

<details>
<summary>Likely follow-up (design first, then reveal)</summary>


One customer is on a burst-heavy usage pattern that keeps tripping the limiter and generating support tickets. What would you change, and what does it cost you?

</details>

### Design a Distributed Cache
*Focus: Caching, Consistency & Trade-offs · ~75 min*

Design a distributed in-memory cache used by many services. Cover eviction policy, partitioning across nodes, and consistency when the underlying data changes.

<details>
<summary>Likely follow-up (design first, then reveal)</summary>


A node in the cache cluster just died. Walk through exactly what happens in the next 30 seconds, and what your users experience.

</details>

### Design a Notification System
*Focus: Scalability, Reliability · ~75 min*

Design a system that sends notifications (email, SMS, push) triggered by events across a product. Cover fan-out, retry/failure handling, and rate limits per user.

<details>
<summary>Likely follow-up (design first, then reveal)</summary>


The SMS provider starts silently dropping 5% of messages with no error response. How would you even detect that, and what's your mitigation?

</details>

### Design a News Feed
*Focus: Data Modeling, Scalability · ~75 min*

Design a social news feed. Cover fan-out-on-write vs. fan-out-on-read, handling users who follow many accounts, and feed ranking at a high level.

<details>
<summary>Likely follow-up (design first, then reveal)</summary>


One account has 50 million followers and posts several times a day. Does your fan-out strategy still hold, and if not, what breaks first?

</details>

### Design a Distributed Job Scheduler
*Focus: Reliability, Consistency & Trade-offs · ~75 min*

Design a system that schedules and reliably executes jobs (cron-like and one-off) across a fleet of workers. Cover exactly-once vs. at-least-once execution and handling a worker crash mid-job.

<details>
<summary>Likely follow-up (design first, then reveal)</summary>


Two workers just picked up the same job at the same time because of a scheduling race. How does your design prevent or recover from that?

</details>

### Design a Chat/Messaging System
*Focus: Consistency & Trade-offs, Scalability · ~75 min*

Design a 1:1 and group messaging system. Cover message ordering, delivery guarantees, read receipts, and how you'd handle a user with a flaky connection.

<details>
<summary>Likely follow-up (design first, then reveal)</summary>


A group chat has 500 members and someone sends a message every second. What's your bottleneck, and how do you keep read receipts from making it worse?

</details>

### Design an Idempotent Payments API
*Focus: API Design, Reliability, Cost & Operational Reasoning · ~75 min*

Design the API and backend for processing payments where retries are expected (client timeouts, network failures). Cover idempotency keys, state machine for a payment's lifecycle, and reconciliation.

<details>
<summary>Likely follow-up (design first, then reveal)</summary>


Finance reports a small number of double-charges last month despite idempotency keys. Where would you actually look, and how would you prevent recurrence?

</details>

### Design Search Autocomplete
*Focus: Caching, Scalability · ~75 min*

Design a typeahead/autocomplete system for a search box. Cover data structure choice (trie vs. precomputed top-k), freshness of suggestions, and latency budget.

<details>
<summary>Likely follow-up (design first, then reveal)</summary>


Trending searches need to show up in suggestions within minutes, not the next daily batch job. What has to change?

</details>

### Design a Log/Metrics Aggregation Pipeline
*Focus: Observability, Scalability, Cost & Operational Reasoning · ~75 min*

Design a pipeline that ingests logs/metrics from thousands of services and makes them queryable. Cover ingestion at scale, storage trade-offs, and how you'd keep it usable during an incident (when volume spikes).

<details>
<summary>Likely follow-up (design first, then reveal)</summary>


Storage costs for this pipeline just became the single largest infra line item. What do you cut, and how do you decide what's safe to lose?

</details>

### Design a Multi-Tenant SaaS Backend
*Focus: Data Modeling, Reliability · ~75 min*

Design the data layer for a B2B SaaS product serving many customers (tenants). Cover tenant isolation strategy, noisy-neighbor risk, and how you'd handle one tenant needing a schema customization.

<details>
<summary>Likely follow-up (design first, then reveal)</summary>


Your single largest customer just asked for a contractual guarantee that their data never shares infrastructure with anyone else. What does that actually cost you to support?

</details>

### Design a File Storage/Sharing Service
*Focus: Data Modeling, Scalability · ~75 min*

Design a service like Dropbox: upload, store, sync, and share files. Cover chunking large files, deduplication, and how sync conflicts get resolved.

<details>
<summary>Likely follow-up (design first, then reveal)</summary>


Two people edit the same file offline on different laptops and reconnect at the same time. Walk through exactly what each of them sees.

</details>

### Design a Leaderboard/Ranking System
*Focus: Data Modeling, Consistency & Trade-offs · ~75 min*

Design a real-time leaderboard for a game or platform with millions of users. Cover the data structure for fast rank lookups and how you'd handle ties and frequent score updates.

<details>
<summary>Likely follow-up (design first, then reveal)</summary>


Someone asks for 'my rank among just my friends,' computed live, not the global leaderboard. Does your data structure still work?

</details>

### Design a Distributed Unique ID Generator
*Focus: Consistency & Trade-offs, Scalability · ~75 min*

Design a service that generates globally unique, roughly time-sortable IDs across many machines without a central bottleneck (Snowflake-style). Cover clock skew and collision avoidance.

<details>
<summary>Likely follow-up (design first, then reveal)</summary>


One data center's clock drifts 200ms behind the others for an hour. What actually breaks, and how would you even notice?

</details>

### Design an On-Call Alerting System
*Focus: Reliability, Observability · ~75 min*

Design a system like PagerDuty: route alerts from monitoring systems to the right on-call engineer, with escalation if unacknowledged. Cover escalation policies, dedup of noisy alerts, and reliability of the alerting path itself.

<details>
<summary>Likely follow-up (design first, then reveal)</summary>


The alerting system itself is down during an incident — the thing meant to page people about outages is having one. How did you design around that, if at all?

</details>

### Design a RAG-Based Q&A System
*Focus: AI / LLM Infrastructure, Data Modeling · ~75 min*

Design a system that answers questions over a large private document set using retrieval-augmented generation. Cover chunking and embedding strategy, vector store choice, how retrieved context gets assembled into the prompt, and what happens when retrieval finds nothing relevant.

<details>
<summary>Likely follow-up (design first, then reveal)</summary>


Users are getting confidently wrong answers when the real answer isn't in the document set at all. How do you detect and fix that class of failure specifically?

</details>

### Design an LLM Serving Gateway
*Focus: AI / LLM Infrastructure, Scalability · ~75 min*

Design a gateway that sits between your product's backend services and one or more LLM providers. Cover request routing across providers/models, timeout and retry behavior, streaming responses, and rate limit handling per provider.

<details>
<summary>Likely follow-up (design first, then reveal)</summary>


Your primary LLM provider has a regional outage during peak traffic. What's your fallback path, and what does the user actually experience?

</details>

### Design a Customer-Support Chatbot on a Third-Party LLM
*Focus: AI / LLM Infrastructure, Reliability · ~75 min*

Design a customer-support chatbot built on top of a third-party LLM platform, with access to order history and support docs. Cover context-window management across a long conversation, escalation to a human agent, and guardrails against the bot making commitments it shouldn't (refunds, promises).

<details>
<summary>Likely follow-up (design first, then reveal)</summary>


The bot just told a customer it would issue a refund it has no authority to approve. How does your design prevent that from happening again, not just this once?

</details>

### Design a Content Moderation Pipeline Using an LLM
*Focus: AI / LLM Infrastructure, Cost & Operational Reasoning · ~75 min*

Design a pipeline that moderates user-generated content (text and images) at scale, using a mix of cheap classifiers and an LLM for ambiguous cases. Cover the cost trade-off between running everything through the LLM versus a tiered approach, latency budget for real-time posting, and human review for edge cases.

<details>
<summary>Likely follow-up (design first, then reveal)</summary>


Volume just tripled overnight after a viral moment, and your LLM moderation costs tripled with it. What do you change in the next hour, versus what you'd change over the next month?

</details>
