# Design a Chat/Messaging System

*Classical Distributed Systems · Focus: Consistency trade-offs, scalability · ~75 min*

## The practice prompt

Design a 1:1 and group messaging system.

## What a strong answer covers

- Message ordering is per-conversation, not global — a meaningfully cheaper guarantee to provide
- Delivery guarantee (usually at-least-once with client-side dedup, not exactly-once)
- How read receipts avoid becoming their own scaling problem in large groups
- Delivering messages correctly to a user who reconnects after being offline

## Rubric

See [the shared rubric](../rubric.md).

## Likely follow-up

<details>
<summary>Design first, then reveal</summary>

A group chat has 500 members and someone sends a message every second. What's your bottleneck, and how do you keep read receipts from making it worse?
</details>
