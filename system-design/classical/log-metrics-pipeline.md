# Design a Log/Metrics Aggregation Pipeline

*Classical Distributed Systems · Focus: Observability, scalability, cost & operational reasoning · ~75 min*

## The practice prompt

Design a pipeline that ingests logs/metrics from thousands of services and makes them queryable.

## What a strong answer covers

- Ingestion architecture that absorbs a volume spike without falling over (buffering, backpressure)
- Hot vs. cold storage trade-off and what it means for query latency on older data
- A sampling strategy and being explicit about what you're willing to lose to control cost
- Keeping the pipeline usable during the exact incident that's generating the volume spike

## Rubric

See [the shared rubric](../rubric.md).

## Likely follow-up

<details>
<summary>Design first, then reveal</summary>

Storage costs for this pipeline just became the single largest infra line item. What do you cut, and how do you decide what's safe to lose?
</details>
