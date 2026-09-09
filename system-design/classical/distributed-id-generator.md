# Design a Distributed Unique ID Generator

*Classical Distributed Systems · Focus: Consistency trade-offs, scalability · ~75 min*

## The practice prompt

Design a service that generates globally unique, roughly time-sortable IDs across many machines without a central bottleneck.

## What a strong answer covers

- Why a central auto-increment doesn't scale, and what replaces it (Snowflake-style: timestamp + machine ID + sequence)
- Clock skew's effect on time-sortability specifically
- Collision avoidance across machines without requiring coordination on every ID
- What happens at ID exhaustion or sequence rollover under high throughput

## Rubric

See [the shared rubric](../rubric.md).

## Likely follow-up

<details>
<summary>Design first, then reveal</summary>

One data center's clock drifts 200ms behind the others for an hour. What actually breaks, and how would you even notice?
</details>
