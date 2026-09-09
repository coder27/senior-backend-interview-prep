# Design a Distributed Cache

*Classical Distributed Systems · Focus: Caching, consistency trade-offs · ~75 min*

## The practice prompt

Design a distributed in-memory cache used by many services.

## What a strong answer covers

- Eviction policy choice (LRU/LFU/TTL) matched to the actual access pattern
- Partitioning strategy (consistent hashing) and what happens on node failure or rebalance
- Cache invalidation strategy and the staleness window it implicitly creates
- Thundering-herd protection when a single hot key expires under heavy concurrent load

## Rubric

See [the shared rubric](../rubric.md).

## Likely follow-up

<details>
<summary>Design first, then reveal</summary>

A node in the cache cluster just died. Walk through exactly what happens in the next 30 seconds, and what your users experience.
</details>
