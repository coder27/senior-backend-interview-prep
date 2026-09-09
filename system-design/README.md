# System design prompts

Each prompt is its own file — read one at a time, not the whole set in one sitting.

[`rubric.md`](rubric.md) applies to every prompt below.

## AI Production Systems

The point of this repo. Production AI system design — serving, evaluation, observability, guardrails — reached general senior backend loops in 2026, and most existing prep material is still teaching 2023-era RAG-101. Each file here explains the actual mechanism (with a diagram), not just a checklist of buzzwords to mention.

- [Design a RAG-Based Q&A System](ai-production/rag-based-qa-system.md)
- [Design an LLM Serving Gateway](ai-production/llm-serving-gateway.md)
- [Design a Customer-Support Chatbot on a Third-Party LLM](ai-production/customer-support-chatbot-llm.md)
- [Design a Content Moderation Pipeline Using an LLM](ai-production/content-moderation-pipeline.md)
- [Design an AI Observability & Monitoring Platform](ai-production/ai-observability-platform.md)
- [Design a Multi-Model Routing & Fallback System](ai-production/multi-model-routing-fallback.md)
- [Design a Production AI Agent Platform with Guardrails](ai-production/production-agent-guardrails.md)
- [Design an LLM Evaluation Pipeline](ai-production/llm-evaluation-pipeline.md)

## Classical Distributed Systems

The evergreen fundamentals. Still worth practicing, not what makes this repo different from [the alternatives](../resources.md) — these are lighter treatments (a checklist and a follow-up, not a full mechanism write-up).

- [Design a URL Shortener](classical/url-shortener.md)
- [Design a Rate Limiter](classical/rate-limiter.md)
- [Design a Distributed Cache](classical/distributed-cache.md)
- [Design a Notification System](classical/notification-system.md)
- [Design a News Feed](classical/news-feed.md)
- [Design a Distributed Job Scheduler](classical/distributed-job-scheduler.md)
- [Design a Chat/Messaging System](classical/chat-messaging-system.md)
- [Design an Idempotent Payments API](classical/idempotent-payments-api.md)
- [Design Search Autocomplete](classical/search-autocomplete.md)
- [Design a Log/Metrics Aggregation Pipeline](classical/log-metrics-pipeline.md)
- [Design a Multi-Tenant SaaS Backend](classical/multi-tenant-saas-backend.md)
- [Design a File Storage/Sharing Service](classical/file-storage-service.md)
- [Design a Leaderboard/Ranking System](classical/leaderboard-system.md)
- [Design a Distributed Unique ID Generator](classical/distributed-id-generator.md)
- [Design an On-Call Alerting System](classical/oncall-alerting-system.md)
